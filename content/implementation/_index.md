---
title: "💻 Implementation"
description: "How we implemented key aspects of NudgeMe."
layout: single
image: "images/system-design/gears.png"
date: 2021-03-09
draft: false
---

# Client-side

Below are details of how we implemented key parts of the mobile application.

## PDF Generation

We want to generate a PDF of the user's wellbeing graph, and allow them to
share it.
We use two libraries - pdf and printing - to generate a PDF of a widget.

At first, this _seems_ easy.
These libraries allow us to easily share a PDF that contains some image.
We just have to create the document, add a page that contains an image
and save the document. Here is the relevant method in our sharing class:

``` dart

    void _share() async {
        final doc = pw.Document(); // create new document

        // Get image source, we implement _fromWidgetKey() ourselves:
        final ImageProvider flutterImg = await _fromWidgetKey(); 

        // convert the image source into a format recognised by the pdf library:
        final pw.ImageProvider img = await flutterImageProvider(flutterImg); 

        // adds an a4 page containing the image at the center
        doc.addPage(pw.Page(
            pageFormat: PdfPageFormat.a4,
            build: (pw.Context ctx) => pw.Center(child: pw.Image.provider(img))));

        // opens the share panel, allowing the user to share the newly
        // created document
        await Printing.sharePdf(bytes: doc.save(), filename: _filename);
    }

```

The problem (and interesting part) is how we get an image (i.e. how to implement 
the `_fromWidgetKey()` method). Firstly, the 
'image' that we wish to share is the image of the user's wellbeing graph. However, 
this is *not* actually an 'image' (yet), it is a visual component of the UI 
built and drawn by Flutter.

To convert an arbitrary widget to an image, it must first be wrapped around a
`RepaintBoundary` widget. From the docs:

> `RepaintBoundary`
> Creates a widget that isolates repaints.

This then allows us to capture the state of the widget and convert it to an image.
As usual in Flutter, we will use a key (which acts a bit like a pointer) so we
can perform the conversion when needed. Here is a bit of code from the wellbeing 
graph:

``` dart

    // this is from the _getGraph method in wellbeing_graph.dart
    return Flexible(
        child: RepaintBoundary(
            // wraps it in a [RepaintBoundary] so we can use .toImage()
            key: _printKey, // this [RepaintBoundary] will be 'printed'/shared
            child: charts.BarChart(

```

There is one more part before we can define `_fromWidgetKey()`. The PDF library
requires an `ImageProvider`, not an `Image`[^1], which is what `.toImage()` will
return. However, we can convert an `Image` by taking it's byte data and creating
an `ImageProvider` from it's raw byte data.

This is the implementation of `_fromWidgetKey()`:
``` dart

  /// will get an [ImageProvider] for the widget associated with _printKey
  Future<ImageProvider> _fromWidgetKey() async {
    // gets the RenderObject associated with the RepaintBoundary pointed to by _printKey:
    final RenderRepaintBoundary wrappedWidget =
        _printKey.currentContext.findRenderObject();
    final img = await wrappedWidget.toImage();

    // needs to be a PNG format, otherwise the conversion won't work
    final byteData = await img.toByteData(format: ImageByteFormat.png);
    return MemoryImage(byteData.buffer.asUint8List());
  }

```

[^1]: The difference is that `ImageProvider` is a way to identify or reference an
      image, but `Image` is an actual image asset.

## Public Key Cryptography

## Database & Notifier/Listener Abstraction

# Server-side

Below are details of how we implemented key parts of the backend server.

## Caching Wellbeing Data
