# Developing

- Edit markdown as needed in `content/`. `data/` is for
the components of a page like a video or Figma embed.
- Run `hugo server`.
- Navigate to the URL displayed in the command line, the site
should update and you can see your changes locally.

# Deployment

In the project root directory:
``` sh
hugo -D
scp -r public/* $USERNAME@knuckles.cs.ucl.ac.uk:/cs/student/www/2020/group26
```
Make sure to set the username.
