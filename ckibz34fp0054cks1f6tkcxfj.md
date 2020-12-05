## Sass Setup for Visual Studio Code


Photo by Halacious on Unsplash

## **What is SASS?**

[Sass](https://sass-lang.com/) is the most mature, stable, and powerful professional grade CSS extension language in the world. In other words, it’s CSS with superpowers.

## **Setting Up Sass in Visual Studio Code**

1. Open Visual Studio Code and go to extensions.

1. Search Live Sass Compiler and Install it.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1607189417661/Zie1yHSpz.png)

3. Now press F1, search for Preferences.

4. Open **Preferences: Open Settings (JSON)**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1607189419303/LYyoELsz3.png)

5. Now add the following snippet at the top of settings.json (you can customize the options to your liking [refer this link](https://ritwickdey.github.io/vscode-live-sass-compiler/docs/settings.html))

```
"liveSassCompile.settings.formats": [

// More Complex

{

"format": "compressed",

"extensionName": ".min.css",

"savePath": "~/../css/"

}

],

"liveSassCompile.settings.generateMap": false,
```


Note: If you add the same above snippets in your settings.json, then your sass files will compile into the parent directory in a folder named **CSS, **and** **all the CSS files will get compressed and saved with .min.css extension**. **If you like the Sass compiler to behave in some other way than this, you can change the configuration. I like to use the following folder structure

```
index.html
/css
      styles.min.css
/scss
      styles.scss
```


Now you are ready to dive into the world of Sass. Open a .scss or .sass file. Clicking the Watch Sass button at the bottom bar of VSCode will compile sass file to css.

If you like to learn more about Sass magical powers, I highly recommend the Traversy Media [Sass Crash Course](https://www.youtube.com/watch?v=nu5mdN2JIwM).