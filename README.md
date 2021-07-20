# STEP BY STEP PROCEDURE IN CONFIGURING TAILWINDCSS IN YOUR DJANGO PROJECT

## This method is going to use postcss, which is the recommended way. 

- First and foremost, create a direcotry in the root of your django project, I will call mine 'jstoolchain'

- In the jstoolchain directory, run `npm init -y`. This command will generate a package.json file in the jstoolchain directory.

- Next, run `npm install tailwindcss postcss postcss-cli autoprefixer`. This will install all the necessary packages. Don't forget to add the node_modules/ to your .gitignore file. 

- For later customization, you'll need a `tailwind.config.js` file. To create this file, in the jstoolchain directory, run `npx tailwind init`.

- Create a `postcss.config.js` file in the same directory as `tailwind.config.js`. This will be the jstoolchain directory in my case.

- Inside the `postcss.config.js` add the following configuration 
  ```
  module.exports = {
    plugins: [
      require('tailwindcss'),
      require('autoprefixer'),
    ]
  }
  ```
  
- In the jstoolchain directory, create a `css` directory, and in this css directory, create a base css file. Make sure the `css` directory is on the same level as the `tailwind.config.js` file. I will call my base file `tailwind-base.css`.

- Add the following to `css/tailwind-base.css`
  ```
  @tailwind base;
  @tailwind components;
  @tailwind utilities;
  ```
  
- In the `package.json` file, add a build script that will build the css file for usage. Under the `scripts`, add the build script.
  ```
  {
    ...
    "scripts": {
      "build:css": "postcss 'location of the base tailwindcss file' -o 'location of where you want the built css file'"
    }
    ...
  }
  ```
  - Example: 
    ```
      {
        ...
          "scripts": {
            "build:css": "postcss css/tailwind.css -o ../static/css/tailwind/tailwind.css"
          },
        ...
      }
    ```
    
- Now it's time to build it. Change directory into the `jstoolchain` directory and run `npm run build:css`

- Check the output directory to ensure the build css is there.


### Using the built css file in your django project
- In your `base.html` file, add `{% load static %}`. Then in the `<head></head>` tags, add `  <link type="text/css" rel="stylesheet" href="{% static 'location of the built css file' %}">`
