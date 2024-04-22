
# Module 2 - week 4.17

Now we are going to create a Astro-based website. It consists of homepage, blog, projects page, etc. We'll be using Tailwind to build a layout that is responsive and handles dark and bright mode. We'll learn how to use Astro components to compose the HTML, server side, using JavaScript imports. Also, we'll learn how to create dynamic routes and how to use content collections to build the app. 

## Contents

1. Introduction 
1. What is Astro
1. Installing Astro
1. 

## Introduction

In the previous module we talked about what the app will do, we defined the data model, we installed PocketBase, explored it, we created the projects and tasks collections to store data.

In this module we'll introduce Astro that will be our backend framework. We'll create a homepage and a blog where we'll post all the news about our app.

## Goals

- how to use Astro to create a website
- how to use Tailwind CSS to style a web page
- how to use responsive design to build a page that looks great on both desktop and mobile devices
- how to design for dark and bright mode
- how to use Astro components to compose HTML, server-side, using JavaScript imports
- how to create dynamic routes
- how to build a blog in Astro using content collections.

## What is Astro

Astro is a backend framework written in JavaScript (Typescript actually) that you use to build websites and web applications.

What is its role in our applicataion? 

how does it paly with PocketBase?

PocketBase will:

- host data in a SQLite database
- provide model around the database, taking care of things like relations and authorizations
- provide a JavaScript API to query and insert data
- provide tools for authentication
- provide file uploads functionality

Astro will:

- generate the HTML of the website
- render the blog from markdown pages
- generate the HTML of the signup and login forms
- handle aunthenticated requests for users that are logged in
- provide a customized dashboard to each user, gathering from PocketBase the user-specific data
- handle all the HTTP requests the users will generate by clicking around the app in the browser, to create projects, delete projects, add tasks, etc. 

PocketBase is the database server. Astro is the backend server (or application server). 

We'll use Astro on the backend side of our stack because:

- I really like it, compared with other backend JavaScript frameworks, for instance express
- It has a simpler mental model: everything is 'spits out' is HTML
- it plays well with the Web Platform defaults. Do you want to use JavaSript? you add a &lt;script> tag. Do you want to use CSS? you add a &lt;style> tag.
- we can generate the HTML using a syntax similar to JSX (JavaScript EXtensible format used in React for instance)
- it can do both static page rendering and server rendering
- it works with htmx (we wil see...) thanks to its ability to generate HTML partials (and not just full HTML pages)
- it evolves to become more complex, but always it starts as a simple backend tool
- being JavaScript, you can use any NodeJS API or npm package you may need.

 But What Is a Framework?

 NodeJS is a JavaScript runtime environment for running JavaScript applications outside the browser. It is asynchronous. It is event-driven. 

 With around 50,000 open source packages available through npm (Node Package Manager), it offers quite a variety of tools and option in fullstack web development

 So a framework. Nodejs frameworks are a set of libraries, templates, and tools built on top of the Node environment. They offer a basic structure for applications including routes, middleware, and templates that streamline the development process. 

 Why use NodeJS frameworks?

 It provides so called syntactic sugar (easier, simpler looking syntax).

 What does it mean?

 Look at the code snippet below that showcases the displaying of a &lt;h2> tag on the home route using vanilla JavaScript and Express. 

```
//NodeJS
const server = http.createServer((req, res) => {
    res.setHeader('Content-Type', 'text/html');
    res.write('<html>');
    res.write('<head><title>Best NodeJS Frameworks</title><head>');
    res.write('<body><h2>Hello from the Ably Blog</h2></body>');
    res.write('</html>');
    res.end();
});


// Express
const express = require('express');
const app = express();
 
app.get('/', (req, res) => {
    res.send('<h2>Hello from the Ably Blog</h2>');
});
```
In NodeJS, we create an http server, use setHeader to manually set the response content type and write all the required HTML tags to be able to display the &lt;h2> tag.

In Express, we only need to just send the &lt;h2> tag as a response. 

Express is a minimalistic web framework to simplify the backend application development with a robust set of features including routing, middleware, error handling, and templating

NestJS is a framework that uses both JavasCript and Typescript. It follows a modular architecture. The use of modules ensures maintainability and reusability across various parts of the application.



 ref https://ably.com/blog/best-nodejs-frameworks


## Installing Astro Locally

Your workspace should be in either ~/Desktop or ~/Documents folders. The tilde refers to your home location.

Inside you should have a folder ~/Documents/QUARTER_3/dev

cd into ~/Documents/QUARTER_3/dev folder and run 
```
npm create astro@latest
```
You may (or may not) be able to run it on your laptops. It depends on several factors. I will show you how it run when connected to the Internet, where you have access to the most updated versions of all packages and process. If you cannot do it in your laptops, I will show the alternative ways to install it in your laptops.

But first watch Astro installation with access to the Internet:

![](/npm-create-astro-at-latest-command.mp4)
<!-- [![](https://markdown-videos-api.jorgenkh.no/youtube/{video_id})](https://youtu.be/{video_id}) -->
![](/public/npm-create-astro-at-latest-command.mp4)
<video width="320" height="240" controls>
  <source src="npm-create-astro-at-latest-command.mp4" type="video/mp4">
  <source src="npm-create-astro-at-latest-command.mp4" type="video/ogg">
  Your browser does not support the video tag.
</video>

Now in the terminal (within VS Code or not), you can run
```
npm run dev
```

Got to http://localhost:4321, you should see the following:


![](/public/cd-astroapp-ls-cat-config-files.mp4)
<video width="320" height="240" controls>
  <source src="cd-astroapp-ls-cat-config-files.mp4" type="video/mp4">
  <source src="cd-astroapp-ls-cat-config-files.mp4" type="video/ogg">
  Your browser does not support the video tag.
</video>

## About VS Code configuration

Everyone has his/her preferences with code style. You can select your own preferences. Some of the examples are taken from github. If you want your code to match them, use Prettier, a style formatting extension for VS Code. I am not sure if you have it yet. 

In any case, go to the VS Code Settings and enable 'Editor: Format On Save'. The code will auto-format every time you save a file (or automatically if you have auto-save).

Also, you may modify Prettier settings 'Semi' and 'Single Attribute Per Line.

## About Typescript

It is basically JavaScript, but with types support, so we could say 'we expect this value to be a string (an not a number)' or 'this is a number (and not a string)' which JavaScript does not provide out of the box. In this project you will use a lot of inferred types, which means there is a minimal amount of type annotations in some critical places, and then TypeScript fill figure out automatically the rest.

This approach has few advantages:

- code completion in VS Code: a nice development experience or DX that only types can provide
- the TypeScript compiler can warn about possible issues related to types, for example, using a property not defined on a type, or passing the wrong type to a function.


## Overview of the starter Astro site

The page with the 'Welcome to Astro' title in it was generated by Astro, through the file 
```
src/pages/index.astro
```

In Astro components the part between three dashes '---' is server-side code with the import required. After that, there's the HTML rendered in the browser.

The HTML defined in this Astro page component is almost the same you see in the browser, except for the doctype and the head tags, and the Vite (the build tool used by Astro) script which is used in development for hot reloading / automatic refres of the page when you change something in your editor.

Look at the Elements panel of the browser DevTools

## Astro vs other JS frameworks

Astro run server side and generates simple HTML by default. There is no complexity introduced by stuff like virtual DOM, client-side hydration that some frameworks like React, Vue, Svelte introduce.

The biggest difference is that those frameworks are heavy JavaScript applications running inside the browser that drive the user interface.

So the user load a page, some JavaScript is loaded, the JavaScript determines what appears on the page. The so called 'SPA (Single Page App) approach'.

Also, client-side navigation is all controlled by JavaScript.

With Astro, we generate the HTML server side, the browser renders the HTML. Period.

It is how the web worked for decades, before 'modern JS frameworks' started to reinvent a lot of patterns and introduced client-side navigation.

Click a link? The browser makes a request to Astro, it generates new HTML and the browser renders it

Most of the frameworks (React, Svelte, ...) are now trying to go 'back to the server' but the solution for them is far from the simple, bare-bones approach that Astro went into from day 1.

All while not limiting you to use a frontend framework if you want, thanks to its 'islands architecture'. We will pair Astro with an incredible tool (htmx), to get to a level of interactivity that people nowadays link to using a fully featured frontend framework like React.

The combination of the two will let us create SPA-grade applications with a simplicity that will make you wonder why are people dealing with a heavy frontend framework at all. This is a question on one of Flavio Copes blog. And I think the answer lies in the mobile vs non-mobile devices usage.

## Homepage 

Firstly, you are not going to create an award-winning landing page. 

But, it will be something simple and nice to look at. When the app will make some money we may hire a designer.

In light mode: 

![](/head-pic1a.png)
![](/head-after-pic1a.png)
![](/head-after-pic1b.png)
![](/head-after-pic1c.png)
![](/head-after-pic1d.png)
![](/head-after-pic1e.png)


In cark mode: 

![](/dark-1a.png)
![](/dark-1c.png)
![](/dark-1d.png)
![](/dark-1e.png)
![](/dark-1f.png)

Here the view in a mobile device:

<video width="320" height="240" controls>
  <source src="spring24app-mobile-view.mp4" type="video/mp4">
  <source src="spring24app-mobile-view.mp4" type="video/ogg">
  Your browser does not support the video tag.
</video>


We will implement this page from top to bottom.

We are going to use Tailwind CSS. 

Tailwind is a library that makes super easy to style HTML pages using CSS

I will install Tailwind CSS IntelliSense, Docs, Headwind

## Install the Astro Tailwind extension

Back to the terminal, stop the currently running app with the keyboard combination ctrl-c. Run
```
npx astro add tailwind
```
TIP: 

npx is a command we use to run an npm package without installing it first

When prompted press Enter to apply the default options. 
If you can not run npx command, I will provide with the output directly to you through canvas. In short, the script will allow to configure Tailwind in your app. Once you're done, you can restart Astro app with **npm run dev** command

You’ll notice the “Astro” text is now a bit smaller, because Tailwind resets the default browser style when installed (something called preflight), by adding a few initial baseline rules that will help us avoid having to reset any pre-existing applied styles, and start from a blank slate.


## Create a layout

he first thing we’re going to do is, we create a layout for our site HTML rendering structure.

In the src/pages/index.astro file we’re now rendering all the HTML the page will generate.

But a lot of this HTML will be common to other pages as well. So instead of replicating all the HTML, we create a layout, and then we’ll import this layout in our index.astro page.

Create a src/layouts folder.



inside it, create an empty file named <code>LayoutSite.astro</code>:

![]()

Now take everything you have in <code>index.astro</code> and copy it over to <code>LayoutSite.astro</code>:

```
---

---
<html lang='en'>
  <head>
    <meta charset='utf-8' />
    <link rel='icon' type='image/svg+xml' href='/favicon.svg' />
    <meta name='viewport' content='width=device-width' />

    <title>Spring24app</title>
  </head>
  <body>
    <h1>Astro</h1>
  </body>
</html>
```

Now in <code>index.astro</code> you can import <code>LayoutSite.astro</code> at the top, and then you can use the <code>LayoutSite</code> component in the HTML part, like this:

```
---
import LayoutSite from '../layouts/LayoutSite.astro'
---

<LayoutSite />
```

The part between --- is JavaScript/Typescript code.

<code>import</code> in particular is part of what we call 'ES modules' syntax. Import make a file available in another file. The page rendered in the browser is exactly like before: everything in the layout gets printed in <code>src/pages/index.astro</code>.

This is a component, a layout component. Setting parts of the page as components make more easily to build and manage a page, like with legos building a more complex structure. We may have a header component, a pricing component, a navigation component and so on.

<code>&lt;LayoutSite /> </code>is a **self-closing** tag, as it has not content inside it.

We can put a special tag called <code>&lt;slot /></code> in the layout, and everything inside the tags will be put where the <code>&lt;slot /></code> tag is.

Let's do it!!


```
---

---
<html lang='en'>
  <head>
    <meta charset='utf-8' />
    <link rel='icon' type='image/svg+xml' href='/favicon.svg' />
    <meta name='viewport' content='width=device-width' />

    <title>Spring24app</title>
  </head>
  <body>
    <slot />
  </body>
</html>
```
.

```
---
import LayoutSite from '../layouts/LayoutSite.astro'
---
<LayoutSite>
   <h1>Astro</h1>
</LayoutSite>
```

The beauty of this approach is that if you want to create another page in your site, you reuse the layout, but add different content into it, like this:

```
---
import LayoutSite from '../layouts/LayoutSite.astro'
---
<LayoutSite>
   <h1>Another page</h1>
   <p>Test ...</p>
</LayoutSite>
```

In this way we avoid duplication of all the HTML that usually goes into the <code>&lt;head></code> tag of the page, plus any of the common page layout. This of the footer, or the header in the same way.

In order to simplify the import syntax, and avoid setting relative paths of the imports, you can edit the <code>tsconfig.json</code> file and add these new lines:

```
{
  "extends": "astro/tsconfigs/strict",
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@components/*": ["src/components/*"],
      "@layouts/*": ["src/layouts/*"],
      "@lib/*": ["src/lib/*"],
      "@data/*": ["src/data/*"],
      "@src/*": ["src/*"],
    }
  }
}
```
Now you can use this import syntax in <code>src/pages/index.astro</code>

```
---
import LayoutSite from '@layouts/LayoutSite.astro'
---

<LayoutSite>
  <h1>Astro</h1>
</LayoutSite>
```
Since you don't have to use relative URL to access a particular resource, you don't have to think 'where is this or that file in the folder structure, and you can move the file around without breaking the import statements.




# Tips from Flavio Copes

💁‍♂️ TIP: Tailwind is called a “utility framework”. If you already know another framework like Bootstrap, Tailwind is similar but kind of different. Instead of providing you with more CSS classes, like .container or .btn-primary that do not tell you exactly what they do, you have what it’s called utility classes. Like .text-right or .text-left. They tell you precisely what they do. And they just do one thing. In this case, they move the text to the right or left. This is just an example. There are many more of those classes, each applying a single property of CSS rather than many at once as happens with Bootstrap.

