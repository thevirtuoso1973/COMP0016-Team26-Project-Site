---
title: "UI Design"
description: "Explanation of our UI design choices"
layout: ui_design
date: 2021-03-13
image: "images/ui-design/small-ui.png"
draft: false
---

## Sketches 

We began the UI design process by making six rough sketches. These initially were pencil on paper, but they have been copied digitally for this website as the features weren’t very clear on the sketches. These sketches acted as a medium to experiment with the placement of the menu and the home page layout.

We evaluated these sketches using the design principles laid out in the HCI lectures. Using these, we chose the best features from each to create the UI Figma. 

<img src="https://user-images.githubusercontent.com/55795994/111051506-71b47e80-844b-11eb-833c-c59a46a6445a.jpeg" 
alt="First page of UI sketches" 
width="700"/>

<img src="https://user-images.githubusercontent.com/55795994/111051508-72e5ab80-844b-11eb-88c8-c3811d84e54d.jpeg" 
alt="First page of UI sketches" 
width="700"/>

Within these sketches, we primarily focused on implementing the Design Principles of *Visibility, Feedback* and *Mapping*.  

<img width="242" alt="sketch 1" src="https://user-images.githubusercontent.com/55795994/111073444-9f92d500-84d6-11eb-9618-785f087c71e4.png">

<img width="227" alt="sketch4" src="https://user-images.githubusercontent.com/55795994/111073449-a15c9880-84d6-11eb-8a50-e9b490f165fa.png">

<img width="250" alt="sketch5" src="https://user-images.githubusercontent.com/55795994/111073445-9f92d500-84d6-11eb-9c7e-5b4c96a48329.png">

The menu design of sketches 1, 4, 5 (and maybe 6) (all shown above) implement the principle of _Feedback_ well, as the selected page is made clear from the state of the icons. However, they also suffer from _Visibility_ and _Affordance_ issues. 
* In 5, the page icons open a labelled window placed on top of the home page, which can be closed using an x button, and in 4, a drop-down menu opens text buttons with the selected page button highlighted. These are good for feedback but require more taps to navigate away from the home page than a navigation bar. This is not ideal as it violates the _Affordance principle_: the home page is not the most critical or interactive page_ but these layouts present it as if it is the most important.

<img width="223" alt="sketch 2" src="https://user-images.githubusercontent.com/55795994/111073443-9e61a800-84d6-11eb-8ce4-2fd25165ec9b.png">

<img width="227" alt="sketch 4" src="https://user-images.githubusercontent.com/55795994/111073449-a15c9880-84d6-11eb-8a50-e9b490f165fa.png">

<img width="200" alt="sketch 6" src="https://user-images.githubusercontent.com/55795994/111073441-9d307b00-84d6-11eb-82a1-fe60f9efb8c9.png">

Sketches 2, 4 and 6 (above) maintain _Simplicity_ and _Visibility_ as they keep the number of features and the amount of text to a minimum. This makes it obvious what should be done on the home page - a Wellbeing Checkup (because at the time, we did not know that users should access the checkup through a notification). 
* The menu placement on these pages is ordinary. Due to the pages' simplicity, it is evident that the buttons are page menu despite there not being a ‘Menu’ label. 
* The menu design, however, in sketches 2 and 3 suffer from a lack of _Visibility_ and _Feedback_, as the menu icons are identical and do not describe which page they correspond to. Therefore, regardless of which icon is selected, it is not clear which page is open. The icons in sketch 6 are much more descriptive. Consequently, we proceeded with simple menu placement: at the bottom of the page with descriptive icons. 



 <img width="100" alt="sketch 3" src="https://user-images.githubusercontent.com/55795994/111073450-a28dc580-84d6-11eb-916b-e1107ddf13bd.png"> 

* Sketch 3 (above) does not contain this _Simplicity_ or _Visibility_. The page is too cluttered to understand the purpose of this page. We did not proceed with any home page layout choices from sketch 3. 

* The slider in sketch 4 makes it very clear to the user that they should rate their well-being, so we kept the idea of a slider and the minimum number of features, text, and simple menu placement. However, we simplified it to a rating out of 10 as these were our Moscow requirements.

Some other design principles we kept in mind whilst evaluating these sketches include _Mapping_ and _Consistency_. The menu design in sketch 3 suffers from a lack of _Mapping_ as the circular buttons feature requires the user to remember which number in the slideshow maps to each page. The vague identical nature of the menu buttons makes this extremely difficult. In all these designs, the idea was to keep the menu identical on every page to maintain the _Consistency_ principle.  

At the top of this page is our final UI Figma, which implements the most successful parts of our sketches: 

* _Horizontal Navigation Bar Menu_ at the bottom of the page (from sketch 2) <img width="90" alt="sketch 2" src="https://user-images.githubusercontent.com/55795994/111073443-9e61a800-84d6-11eb-8ce4-2fd25165ec9b.png"> <img width="150" alt="nav bar" src="https://user-images.githubusercontent.com/55795994/111073929-b20e0e00-84d8-11eb-87ab-dd2e524ecfa8.png">
 
* _Descriptive menu icons_ (resembling sketch 6) <img width="90" alt="sketch 6" src="https://user-images.githubusercontent.com/55795994/111073441-9d307b00-84d6-11eb-82a1-fe60f9efb8c9.png"> <img width="150" alt="nav bar" src="https://user-images.githubusercontent.com/55795994/111073929-b20e0e00-84d8-11eb-87ab-dd2e524ecfa8.png">

* _Highlighted icon_ for the selected page (from 2 and 3) <img width="70" alt="sketch2" src="https://user-images.githubusercontent.com/55795994/111073443-9e61a800-84d6-11eb-8ce4-2fd25165ec9b.png"> <img width="60" alt="sketch3" src="https://user-images.githubusercontent.com/55795994/111073450-a28dc580-84d6-11eb-916b-e1107ddf13bd.png"> <img width="200" alt="highlighted icon" src="https://user-images.githubusercontent.com/55795994/111078470-77fb3700-84ed-11eb-9d6a-9742acfeeb31.png">

* Using a _slider_ to rate wellbeing (from sketch 4) <img width="90" alt="sketch4" src="https://user-images.githubusercontent.com/55795994/111073449-a15c9880-84d6-11eb-8a50-e9b490f165fa.png"> <img width="100" alt="figma slide" src="https://user-images.githubusercontent.com/55795994/111073902-8ee35e80-84d8-11eb-83ae-4f98dfdef752.png">

We distributed the UI Figma to potential users and received the feedback that the UI was not clustered, the buttons were clear, the colours were pleasing to look at and the pages were easy to navigate to.

<img width="300" src="https://user-images.githubusercontent.com/55795994/111519048-9ad85600-874e-11eb-9e8e-dfdcebfaa4fb.png" alt="Naima alpha testing"/>

## Final UI Design

### Design Changes 
The design of the app has changed since making the UI Figma, technically and visually. 

Once we had become more familiar with the requirements, we added a series of introduction pages to gather setup information and introduce the user to the app.

<img width="800" alt="Screenshot 2021-03-14 at 18 00 20" src="https://user-images.githubusercontent.com/55795994/111079053-27390d80-84f0-11eb-8fbe-743629e6c6f3.png">


We also narrowed down the number of pages to 4:
* Wellbeing Diary
* Home 
* Support Network 
* Settings 

We removed the Publish page in the Figma at the request of our project partner. The Checkup page is now accessed through a notification rather than from the navigation bar.

### Colours
On both the website and the app, we confirmed that the colour schemed we used were colour blind accessible using the resource below [1].

 <img width="800" alt="palettes for colour blind accessibility" src="https://user-images.githubusercontent.com/55795994/111082078-43dc4200-84fe-11eb-8717-32c8e494d73d.png"> 

The circled colours in the image above are the colours we chose for the map, which can be found [here](https://comp0016.cyberchris.xyz/map). They were chosen in order to appear different to people with deuteranopia, protanopia and tritanopia.

We only used four colours in the mobile app, the dark purple and blue that can be seen in the buttons below, a lighter purple background and grey headings. Blue and purple is not a sensitive colour combination for the three most common types of colour blindness. 

<img width="400" alt="NudgeMe Home" src="https://user-images.githubusercontent.com/55795994/111078295-a3c9ed00-84ec-11eb-97be-dee19575ed4b.png"> <img width="400" alt="NudgeMe Network page" src="https://user-images.githubusercontent.com/55795994/111078313-b8a68080-84ec-11eb-94b5-78c50c5bcb5e.png"> 

## References

(1) [How to Use Color Blind Friendly Palettes to Make Your Charts Accessible](https://venngage.com/blog/color-blind-friendly-palette/)
