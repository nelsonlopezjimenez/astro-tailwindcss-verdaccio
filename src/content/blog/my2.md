---
title: Module 2
date: 4/1/2024
---

# Module 2 - week 4.17 - PART A

Now we are going to create a Astro-based website. It consists of homepage, blog, projects page, etc. We'll be using Tailwind to build a layout that is responsive and handles dark and bright mode. We'll learn how to use Astro components to compose the HTML, server side, using JavaScript imports. Also, we'll learn how to create dynamic routes and how to use content collections to build the app.

## Contents

1. [Introduction](#introduction)
1. [Goals](#goals)
1. [What is Astro](#what-is-astro)
1. [Installing Astro locally](#installing-astro-locally)
1. [Install Astro](#install-astro)
1. [Creating folder structure manually](#creating-folder-structure-manually)
1. [Create first Astro page](#create-your-first-page)
1. [Create first static asset](#create-first-static-asset)
1. [Edit astro config mjs file](#edit-astroconfigmjs-file)
1. [Adding TypeScript support](#adding-typescript-support)
1. [Starting Astro application](#starting-astro-application)
1. [Configuring VS Code Prettier extension](#configuring-vs-code-prettier-extension)
1. [About TypeScript](#about-typescript)
1. [Overview of starter Astro site](#overview-of-starter-astro-site)
1. [Astro vs other JS frameworks](#astro-vs-other-js-frameworks)
1. [Astro Homepage](#astro-homepage)
1. [Light mode](#in-light-mode)
1. [Dark mode](#in-dark-mode)
1. [In mobile device](#here-the-view-in-a-mobile-device)
1. [Manual install Astro Tailwind extension](#manual-install-astro-tailwind-extension)
1. [Manual install NodeJS integration](#manual-install-nodejs-integration)
1. [Instal dotenv module](#install-dotenv-module)
1. [Create a layout](#create-a-layout)
1. [Tips from Flavio Copes](#tips-from-flavio-copes)
1. [Module2 part B](#module-2-part-b)

## Introduction

[&rarr; top](#)

In the previous module we talked about what the app will do, we defined the data model, we installed PocketBase, explored it, we created the projects and tasks collections to store data.

In this module we'll introduce Astro that will be our backend framework. We'll create a homepage and a blog where we'll post all the news about our app.

## Goals

[&rarr; top](#)

- how to use Astro to create a website
- how to use Tailwind CSS to style a web page
- how to use responsive design to build a page that looks great on both desktop and mobile devices
- how to design for dark and bright mode
- how to use Astro components to compose HTML, server-side, using JavaScript imports
- how to create dynamic routes
- how to build a blog in Astro using content collections.

## What is Astro

[&rarr; top](#)

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

[&rarr; top](#)

Your workspace should be in either ~/Desktop or ~/Documents folders. The tilde refers to your home location.

Inside you should have a folder ~/Documents/QUARTER_3/dev

cd into ~/Documents/QUARTER_3/dev folder and run

```

npm create astro@latest

```

You may (or may not) be able to run it on your laptops. It depends on several factors. I will show you how it run when connected to the Internet, where you have access to the most updated versions of all packages and process. If you cannot do it in your laptops, I will show the alternative ways to install it in your laptops. In the video you'll see a series of options for the installation. You either choose an option, or hit enter to select the default. The first question is about the app's name, it has to be unique. In the following section I will explain the steps to install Astro manually.

But first watch Astro installation with access to the Internet:

<video width="320" height="240" controls>
  <source src="/video/npm-create-astro-at-latest-command.mp4" type="video/mp4">
  <source src="/video/npm-create-astro-at-latest-command.mp4" type="video/mp4">
  <source src="/video/npm-create-astro-at-latest-command.mp4" type="video/ogg">
  Your browser does not support the video tag.
</video>

## Install Astro

[&rarr; top](#)

First, install the Astro project dependencies inside your project. **IMPORTANT** Astro must be installed locally, not globally. Make sure you are not running <code>npm install -g astro</code>

In <code>~/QUARTER-3/dev</code>folder create a folder by running the command <code>mkdir spring24app</code>.

cd into it and run <code>npm init --yes</code>

Then start the installacion of Astro modules:

```

npm install astro@4.4.4

```

If the command is <code>npm install astro</code>(with no particular version number), it searches for the latest version. If the version's dependencies are not found in verdaccio server the installation of node_modules folder will be aborted since there is not connection to the public registry.

Then, replace any placehoder "scripts" section of your package.json with the following:

<!-- ![](/astro-manual-packagejson-scripts.png) -->
<img src="/image/astro-manual-packagejson-scripts.png" alt="astro-manual-packagejson-scripts.png" width=50% style="border:14px solid pink">

## Creating folder Structure manually

[&rarr; top](#)

Run the following commands inside your spring24app folder

```

mkdir src
mkdir src/pages
mkdir public
touch astro.config.mjs
touch tsconfig.json
touch README.md
touch src/pages/env.d.ts
touch src/pages/index.astro

```

Your folder now should look like this:

<!-- ![](/astro-manual-installation-tree.png) -->

<!-- <img src="" alt="" width=70% style="border: 14px solid pink"> -->

<img src="/image/astro-manual-installation-tree.png" alt="astro-manual-installation-tree.png" width=50% style="border: 14px solid pink">

## Create your first page

[&rarr; top](#)

Edit file <code>index.astro</code> in the path <code>src/pages/index.astro</code>.

For this guide, copy-and-paste the following code snippet (including the <code>---</code> dashes) into your new file:

```

---
// Welcome to Astro! Everything between these triple-dash code fences
// is your "component frontmatter". It never runs in the browser.
console.log('This runs in your terminal, not the browser!');
---
<!-- Below is your "component template." It's just HTML, but with
     some magic sprinkled in to help you build great templates. -->
<html>
  <body>
    <h1>Hello, World!</h1>
    <h2>Welcome to Astro!</h2>
  </body>
</html>
<style>
  h1 {
    color: orange;
  }
</style>

```

## Create first static asset

[&rarr; top](#)

In the <code>public/</code> directory you will store static assets. Astro will always include these assets in your final build, so you can safely reference them from inside your component templates.

Create a new file in <code>public/robots.txt</code>. This file is a simple file that most wites will include to tell search bots ike Google how to treat your site.

For this guide, copy-and-paste the following code snippet into your new file:

```

# Example: Allow all bots to scan and index your site.

# Full syntax: https://developers.google.com/search/docs/advanced/robots/create-robots-txt

User-agent: *
Allow: /

```

## Edit astro config mjs file

[&rarr; top](#)

Astro is configured using <code>astro.config.mjs</code>. This file is optional if you do not need to configure Astro, but you may wish to create it now.

```

import { defineConfig } from 'astro/config';

// https://astro.build/config
export default defineConfig({});

```

If you want to include UI framework components such as React, Svelte, etc. or use other tools such as Tailwind or Partytown in your project, here is where you will manually import and configure integrations.

## Adding Typescript support

[&rarr; top](#)

Typescript is configured using <code>tsconfig.json</code>. This file allows Astro and VS Code know how to understand your project.

If you do intend to write TypeScript code, using Astro's <code>strict</code> or <code>strictest</code> template is **recommended**

Edit <code>tsconfig.json</code> at the root of your project:

```

{
  "extends": "astro/tsconfigs/base"
}

```

Finally, edit <code>src/env.d.ts</code> to let TypeScript know about ambien types available in an Astro project:

```

/// <reference types="astro/client" />

```

## Starting Astro application

[&rarr; top](#)

Now in the terminal (within VS Code or not), you can run

```

npm run dev

```

Got to http://localhost:4321, you should see the following:

<!-- ![](/cd-astroapp-ls-cat-config-files.mp4) -->
<video width="320" height="240" controls>
  <source src="/video/cd-astroapp-ls-cat-config-files.mp4" type="video/mp4">
  <source src="/video/cd-astroapp-ls-cat-config-files.mp4" type="video/ogg">
  Your browser does not support the video tag.
</video>

## Configuring VS Code Prettier extension

[&rarr; top](#)

Everyone has his/her preferences with code style. You can select your own preferences. Some of the examples are taken from github. If you want your code to match them, use Prettier, a style formatting extension for VS Code. I am not sure if you have it yet.

In any case, go to the VS Code Settings and enable 'Editor: Format On Save'. The code will auto-format every time you save a file (or automatically if you have auto-save).

Also, you may modify Prettier settings 'Semi' and 'Single Attribute Per Line.

## About TypeScript

[&rarr; top](#)

It is basically JavaScript, but with types support, so we could say 'we expect this value to be a string (and not a number)' or 'this is a number (and not a string)' which JavaScript does not provide out of the box. In this project you will use a lot of inferred types, which means there is a minimal amount of type annotations in some critical places, and then TypeScript fill figure out automatically the rest.

This approach has few advantages:

- code completion in VS Code: a nice development experience or DX that only types can provide
- the TypeScript compiler can warn about possible issues related to types, for example, using a property not defined on a type, or passing the wrong type to a function.

## Overview of starter Astro site

[&rarr; top](#)

The page with the 'Welcome to Astro' title in it was generated by Astro, through the file

```

src/pages/index.astro

```

In Astro components the part between three dashes '---' is server-side code with the import required. After that, there's the HTML rendered in the browser.

The HTML defined in this Astro page component is almost the same you see in the browser, except for the doctype and the head tags, and the Vite (the build tool used by Astro) script which is used in development for hot reloading / automatic refresh of the page when you change something in your editor.

Look at the Elements panel of the browser DevTools

## Astro vs other JS frameworks

[&rarr; top](#)

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

## Astro Homepage

[&rarr; top](#)

Firstly, you are not going to create an award-winning landing page.

But, it will be something simple and nice to look at. When the app will make some money we may hire a designer.

## In light mode

[&rarr; top](#)

<!-- ![Image 1a](/Public/head-pic1a.png) -->

<!-- <img src="" alt="" width=70% style="border: 14px solid pink"> -->

<img src="/image/head-pic1a.png" alt="/head-pic1a.png" width=70% style="border: 14px solid pink">
<img src="/image/head-after-pic1a.png" alt="/head-after-pic1a.png" width=70% style="border: 14px solid pink">
<img src="/image/head-after-pic1b.png" alt="/head-after-pic1b.png" width=70% style="border: 14px solid pink">
<img src="/image/head-after-pic1c.png" alt="/head-after-pic1c.png" width=70% style="border: 14px solid pink">
<img src="/image/head-after-pic1d.png" alt="/head-after-pic1d.png" width=70% style="border: 14px solid pink">
<img src="/image/head-after-pic1e.png" alt="/head-after-pic1e.png" width=70% style="border: 14px solid pink">

## In dark mode

[&rarr; top](#)

<!-- <img src="" alt="" width=70% style="border: 14px solid pink"> -->
<img src="/image/dark-1a.png" alt="dark-1a.png" width=70% style="border: 14px solid pink">
<img src="/image/dark-1c.png" alt="dark-1c.png" width=70% style="border: 14px solid pink">
<img src="/image/dark-1d.png" alt="dark-1d.png" width=70% style="border: 14px solid pink">
<img src="/image/dark-1e.png" alt="dark-1e.png" width=70% style="border: 14px solid pink">
<img src="/image/dark-1f.png" alt="dark-1f.png" width=70% style="border: 14px solid pink">

## Here the view in a mobile device

[&rarr; top](#)

<video width="320" height="240" controls>

  <source src="/video/spring24app-mobile-view.mp4" type="video/mp4">
  <!-- <source src="/image/public/spring24app-mobile-view.mp4" type="video/mp4"> -->
  <source src="/video/spring24app-mobile-view.mp4" type="video/ogg">
  Your browser does not support the video tag.
</video>

We will implement this page from top to bottom.

We are going to use Tailwind CSS.

Tailwind is a library that makes super easy to style HTML pages using CSS

I will install Tailwind CSS IntelliSense, Docs, Tailwind

## Manual Install Astro Tailwind extension

[&rarr; top](#)

Back to the terminal, stop the currently running app with the keyboard combination ctrl-c. Run

```

npx astro add tailwind

```

TIP:

npx is a command we use to run an npm package without installing it first. **IF NPX DOES NOT WORK, JUMP INTO NEXT SECTION: "TAILWIND MANUAL INSTALL"**

When prompted press Enter to apply the default options.
If you can not run npx command, I will provide with the output directly to you through canvas. In short, the script will allow to configure Tailwind in your app. Once you're done, you can restart Astro app with **npm run dev** command

You’ll notice the “Astro” text is now a bit smaller, because Tailwind resets the default browser style when installed (something called preflight), by adding a few initial baseline rules that will help us avoid having to reset any pre-existing applied styles, and start from a blank slate.

1. **Tailwind Manual Install**

[https://docs.astro.build/en/guides/integrations-guide/tailwind/ ](https://docs.astro.build/en/guides/integrations-guide/tailwind/)

At the root of your project run:

```

npm install tailwindcss@3.4.1 @astrojs/tailwind@5.1.0

```

Then, apply the integration to astro.config.mjs file using the <code>integrations</code> property:

<!-- ![](/astro-config-mjs-edit-1a.png) -->
<!-- <img src="" alt="" width=70% style="border: 14px solid pink"> -->
<img src="/image/astro-config-mjs-edit-1a.png" alt="/astro-config-mjs-edit-1a.png" width=70% style="border: 14px solid pink">

Then, create <code>tailwind.config.mjs</code> file at the root of your project. You can use the command **<code>npx tailwindcss init</code>** but since it is not sure just create the file and enter the following code:

```

/** @type {import('tailwindcss').Config} */
export default {
  content: ['./src/**/*.{astro,html,js,jsx,md,mdx,svelte,ts,tsx,vue}'],
  theme: {
    extend: {},
  },
  plugins: [],
};

```

## Manual install NodeJS integration

[&rarr; top](#)

Nodejs is a JavaScript runtime for server-side code. @astrojs/node can be use either in standalone mode or as middleware for other http servers, such as express.

Reference [https://docs.astro.build/en/guides/integrations-guide/node/](https://docs.astro.build/en/guides/integrations-guide/node/)

You can do automatic installation using the command <code>npx astro add node</node>. Just in case, here is the manual install steps:

```

npm install @astrojs/node@8.2.3

```

edit your **astro.config.mjs** file:

```

import { defineConfig } from 'astro/config';
import node from '@astrojs/node';

export default defineConfig({
  output: 'server',
  adapter: node({
    mode: 'standalone',
  }),
});

```

## Install dotenv module

[&rarr; top](#)

```

npm install dotenv@16.4.5

```

## Create a layout

[&rarr; top](#)

he first thing we’re going to do is, we create a layout for our site HTML rendering structure.

In the src/pages/index.astro file we’re now rendering all the HTML the page will generate.

But a lot of this HTML will be common to other pages as well. So instead of replicating all the HTML, we create a layout, and then we’ll import this layout in our index.astro page.

Create a src/layouts folder.

inside it, create an empty file named <code>LayoutSite.astro</code>:

here goes image

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

[&rarr; top](#)

💁‍♂️ TIP: Tailwind is called a “utility framework”. If you already know another framework like Bootstrap, Tailwind is similar but kind of different. Instead of providing you with more CSS classes, like .container or .btn-primary that do not tell you exactly what they do, you have what it’s called utility classes. Like .text-right or .text-left. They tell you precisely what they do. And they just do one thing. In this case, they move the text to the right or left. This is just an example. There are many more of those classes, each applying a single property of CSS rather than many at once as happens with Bootstrap.

## MODULE 2 PART B

[&rarr; top](#)

### Former Module 2a - week 4.17 (cont)

We created a Astro-based website. It consists of homepage, and some other pages (layout pages). We installed Tailwind, Tailwindcss, integration to node, and manually edited configuration files.
we discussed Astro versus other JavaScript frameworks.

We'll be using Tailwind to build a layout that is responsive and handles dark and bright mode. We'll learn how to use Astro components to compose the HTML, server side, using JavaScript imports. Also, we'll learn how to create dynamic routes and how to use content collections to build the app.

## Contents

[&rarr; top](#)

1. [We created a simple layout page]
1. [The top bar](#the-top-bar)
1. [Dark mode](#dark-mode)
1. [The hero section](#the-hero-section)
1. [Screenshot of the app in action](#the-screenshot-of-the-app-in-action)
1. [The feature list](#the-feature-list)
1. [Improving the Feature component using JavaScript](#improving-the-features-component-using-javascript)
1. [Testimonials](#the-testimonials)
1. [The pricing section](#the-pricing-section)
1. [Frequently asked questions](#frequently-asked-questions)
1. [The footer](#the-footer)
1. [Create the blog](#create-the-blog)
1. [Create a collection](#create-a-collection)
1. [Create the blog post list](#create-the-blog-post-list)
1. [The single blog post view](#list-the-latest-blog-post-in-the-homepage)
1. [Wrapping module 2](#wrapping-module-2)
1. [Troubleshooting](#troubleshooting)

## Previously...

At the end of the previous document you imported the first component into src/pages/index.astro file as follows:

```

import LayoutSite from '@layouts/LayoutSite.astro';

<LayoutSite>
    <h1>Astro</h1>
</LayoutSite>

```

## The top bar

[&rarr; top](#)

Let’s add the top bar now.

The top bar includes the site logo, a few navigation links, and a
link to the login page.

We’ll need the top bar in all pages of the site.

Inside **src/components/** folder we’re going to have a lot of components, so we’d better
think about organizing them nicely.

Our Astro site will handle both the public-facing site, and the web app part, so the first big organization is to separate them into **site** and **app** components.

Inside **src/components/site** we can further organize by creating a **common** folder to host components reused across all the website
(like the top bar component) and a **homepage** folder that will host only components related to the homepage, our most complicated
page.

<img class="myMd" src="/image/_image2AA.webp" alt="src folder structure" width=70% />

Inside **common** create the file **TopBar.astro**.

Import it in LayoutSite.astro , and include it right before the &lt;slot />:

```
---
import TopBar from '@components/site/common/TopBar.astro'
---

<html lang='en'>
  <head>
    <meta charset='utf-8' />
    <link rel='icon' type='image/svg+xml' href='/favicon.svg' />
    <meta name='viewport' content='width=device-width' />
    <title>Secretplan</title>
  </head>
  <body>
    <TopBar />
    <slot />
  </body>
</html>

```

Now write “Top Bar” in the TopBar.astro component, and it will
appear in the website:

<img class="myMd" src="/image/_image2AB.webp" alt="topbar with astro title" width=70% />

The logo1 is in the public folder of the Astro site:

Anything in the public folder is statically served from Astro, this means you can access it using as http://localhost:4321/logo1.svg.

Inside your components you can reference it as

```

<img src='/logo.svg' />

```

Save this into TopBar.astro:

```

<nav class='flex justify-between p-6 text-sm font-semibold'>
  <a href='/' class='flex-1'>
    <img src='/logo.svg' alt='Logo' class='h-5 invert dark:invert-0' />
  </a>

  <div class='hidden md:flex gap-x-12'>
    <a href='/#features'>Features</a>
    <a href='/#pricing'>Pricing</a>
    <a href='/blog'>Blog</a>
  </div>

  <div class='flex-1 text-right'>
    <a href='/login'>Log in &rarr;</a>
  </div>
</nav>

```

We have a bunch of HTML tags.

Everything is wrapped in a <nav> tag, which semantically represents a section of a page that links to other pages or to parts within the page.

We use a lot of classes. This is Tailwind CSS in action.

Stripped down, the pure HTML looks like this:

```
<nav>
  <a href='/'>
    <img src='/logo.svg' alt='Logo' />
  </a>

  <div>
    <a href='/#features'>Features</a>
    <a href='/#pricing'>Pricing</a>
    <a href='/blog'>Blog</a>
  </div>

  <div>
    <a href='/login'>Log in &rarr;</a>
  </div>
</nav>

```

The links point to locations we’ll create later on. In particular, **/login** and **/blog** are different pages (we’ll build blog later in this module). **/#pricing** and **/#features** will be locations in the homepage where people can find information about (guess what) the features and the pricing.

An important class we use, that determines how the whole component looks like, is **flex**. This enables flexbox on the &lt;nav> tag.

**justify-between** equally separates the 3 children of nav.

The **flex-1** class on the first and last makes sure they expand to equally take the space remaining, so one stays left, one right.

The middle part, we only show it when the screen is large enough, using hidden **md:flex**.

Then the each individual link is separated from each other using **gap-x-12**.

This is the result:

<img class="myMd" src="/image/_image2AC.webp" alt="_image2AC.webp" width=100%>

(if you don’t see the logo, is your OS in dark mode? try switching to light mode)
When the window is a little bit larger, you’ll see the central menu items too, which are hidden and only shown on medium sized screens:

<img class="myMd" src="/image/_image2AD.webp" alt="_image2AD.webp" width=100%>

## Dark mode

[&rarr; top](#)

If you use dark mode in your OS you don’t see the logo, because the logo is white. In light mode we invert it to black using the invert class, but we revert the invert in dark mode using **dark:invert-0.**

<!-- ![]('/public/_image-4.webp') -->

<img class="myMd" src="/image/_image-4.webp" alt="/_image-4.webp" width=100%>

We fix this by using a dark background in dark mode, and by setting the font white using **dark:bg-black dark:text-white** on the body:

```

---
import TopBar from '@components/site/common/TopBar.astro'
---

<html lang="en">
  <head>
    ...
  </head>
  <body>
  <body class="dark:bg-black dark:text-white">
    <div class="max-w-5xl px-4 py-4 mx-auto">
      <TopBar />
      <slot />
    </div>
  </body>
</html>

```

<img class="myMd" src="/image/_image-5.webp" alt="/_image-5.webp" width=100%>
<!-- ![]('/_image-5.webp') -->

We also set some padding on an inner div, the max width with max-w-5xl, and mx-auto to center this into the page.

I highly encourage you to search on the Tailwind CSS official documentation what those classes do. I do this all the time for classes I don’t remember.

## The hero section

[&rarr; top](#)

Create **src/components/site/homepage/Hero.astro** file. Add the following content:

```

<div>
  <div class='px-6 lg:px-8 max-w-2xl mx-auto text-center'>
    <p>
      <img
        src='/logo.svg'
        alt='Logo'
        class='h-16 mx-auto my-20 invert dark:invert-0'
      />
    </p>

    <h1
      class='text-4xl font-bold tracking-tight sm:text-6xl'>
      The easiest way to manage your projects
    </h1>

    <p
      class='mt-10 mb-5 text-xl text-center md:text-2xl dark:text-zinc-300'>
      A modern solution for all your organization trouble.
      We take the hassle out of managing your projects so
      you can focus on what matters.
    </p>

    <div class='mx-auto mt-12'>
      <a
        href='/#pricing'
        class='rounded-md bg-blue-600 px-3.5 py-2.5 text-xl font-semibold text-white hover:bg-blue-500'>
        Create account
      </a>
    </div>
  </div>
</div>

```

This component is just HTML with some Tailwind CSS classes.

As an exercise, try removing classes and see what happens. You won't learn until you start messing with the code.

Include this is **/src/pages/index.astro**:

```

---
import LayoutSite from '@layouts/LayoutSite.astro'

import Hero from '@components/site/homepage/Hero.astro'
---

<LayoutSite>
  Astro
  <Hero />
</LayoutSite>

```

<img class="myMd" src="/image/_image-6.webp" alt="6" width=100%>
<!-- ![]('/_image-6.webp') -->

## The screenshot of the app in action

[&rarr; top](#)

Let’s now add a big screenshot of the app in action. We haven’t built the app yet, but suppose we have the designs our designer provided us.

Use this screenshot image:

<!-- ![]('/head-after-pic1a.png') -->

<img class="myMd" src="/image/head-after-pic1a.png" alt="/pic1a" width=100%>

Create **src/components/site/homepage/Screenshot.astro**

```

<div class='mt-16 sm:mt-24'>
  <div
    class='p-4 rounded-xl bg-gray-100 ring-1 ring-gray-200 lg:rounded-2xl'>
    <img
      src='/head-after-pic1a.png'
      alt='App screenshot'
      width='2168'
      height='1792'
      class='rounded-md'
    />
  </div>
</div>

```

Include it in your **src/pages/index.astro** file:

```

---
import LayoutSite from '@layouts/LayoutSite.astro'

import Hero from '@components/site/homepage/Hero.astro'
import Screenshot from '@components/site/homepage/Screenshot.astro'
---

<LayoutSite>
  <Hero />
  <Screenshot />
</LayoutSite>

```

Here we go:

<img class="myMd" src="/image/_image-7.webp" alt="" width=100%>
<!-- ![]('/_image-7.webp.png') -->

## The feature list

[&rarr; top](#)

Let’s now add the features list.

This is the end result we want:

<img class="myMd" src="/image/_image-7.webp.png" alt="" width=100%>
<!-- ![]('/_image-7.png') -->

When the screen gets smaller:

<img class="myMd" src="/image/_image-9.webp" alt="" width=100%>
<!-- ![]('/_image-9.png') -->

Here’s the code to make this work. Suppose your designer handed it to you, or you got this generated from a tool like Figma.

Add this HTML to **src/components/site/homepage/Features.astro**:

```

<a id="features"></a>

<div class="px-6 mx-auto mt-32 max-w-7xl sm:mt-56 lg:px-8">
  <div class="max-w-2xl mx-auto lg:text-center">
    <h2 class="text-xl font-semibold leading-7">Ship faster</h2>
    <p class="mt-2 text-3xl font-bold tracking-tight sm:text-5xl">
      Manage your projects more productively
    </p>
    <p class="mt-6 text-lg leading-8">
      With its simple interface and useful features, SECRETPLAN is the best way
      to manage your projects.
    </p>
  </div>
  <div class="max-w-2xl mx-auto mt-16 sm:mt-20 lg:mt-24 lg:max-w-4xl">
    <dl
      class="max-w-xl grid grid-cols-1 gap-x-8 gap-y-10 lg:max-w-none lg:grid-cols-2 lg:gap-y-16">
      <div class="relative pl-16">
        <dt class="text-base font-semibold leading-7">
          <div
            class="absolute top-0 left-0 flex items-center justify-center w-10 h-10 bg-blue-600 rounded-lg">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
              <path stroke-linecap="round" stroke-linejoin="round" d="M15.75 6a3.75 3.75 0 1 1-7.5 0 3.75 3.75 0 0 1 7.5 0ZM4.501 20.118a7.5 7.5 0 0 1 14.998 0A17.933 17.933 0 0 1 12 21.75c-2.676 0-5.216-.584-7.499-1.632Z" />
            </svg>
          </div>
          Solo projects
        </dt>
        <dd class="mt-2 text-base leading-7">
          The solo plan is perfect for freelancers working on projects on their
          own
        </dd>
      </div>
      <div class="relative pl-16">
        <dt class="text-base font-semibold leading-7">
          <div
            class="absolute top-0 left-0 flex items-center justify-center w-10 h-10 bg-blue-600 rounded-lg">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
            <path stroke-linecap="round" stroke-linejoin="round" d="M3.75 21h16.5M4.5 3h15M5.25 3v18m13.5-18v18M9 6.75h1.5m-1.5 3h1.5m-1.5 3h1.5m3-6H15m-1.5 3H15m-1.5 3H15M9 21v-3.375c0-.621.504-1.125 1.125-1.125h3.75c.621 0 1.125.504 1.125 1.125V21" />
            </svg>
          </div>
          Team projects
        </dt>
        <dd class="mt-2 text-base leading-7">
          The team plan is perfect for small teams working together on multiple
          projects
        </dd>
      </div>
      <div class="relative pl-16">
        <dt class="text-base font-semibold leading-7">
          <div
            class="absolute top-0 left-0 flex items-center justify-center w-10 h-10 bg-blue-600 rounded-lg">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
            <path stroke-linecap="round" stroke-linejoin="round" d="m3.75 13.5 10.5-11.25L12 10.5h8.25L9.75 21.75 12 13.5H3.75Z" />
            </svg>
          </div>
          Fast and easy
        </dt>
        <dd class="mt-2 text-base leading-7">
          No more overcomplicated project management
        </dd>
      </div>
      <div class="relative pl-16">
        <dt class="text-base font-semibold leading-7">
          <div
            class="absolute top-0 left-0 flex items-center justify-center w-10 h-10 bg-blue-600 rounded-lg">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">

            <path stroke-linecap="round" stroke-linejoin="round" d="M20.25 8.511c.884.284 1.5 1.128 1.5 2.097v4.286c0 1.136-.847 2.1-1.98 2.193-.34.027-.68.052-1.02.072v3.091l-3-3c-1.354 0-2.694-.055-4.02-.163a2.115 2.115 0 0 1-.825-.242m9.345-8.334a2.126 2.126 0 0 0-.476-.095 48.64 48.64 0 0 0-8.048 0c-1.131.094-1.976 1.057-1.976 2.192v4.286c0 .837.46 1.58 1.155 1.951m9.345-8.334V6.637c0-1.621-1.152-3.026-2.76-3.235A48.455 48.455 0 0 0 11.25 3c-2.115 0-4.198.137-6.24.402-1.608.209-2.76 1.614-2.76 3.235v6.226c0 1.621 1.152 3.026 2.76 3.235.577.075 1.157.14 1.74.194V21l4.155-4.155" />

            </svg>
          </div>
          Multiplayer mode
        </dt>
        <dd class="mt-2 text-base leading-7">
          Work on projects with your colleagues
        </dd>
      </div>
    </dl>
  </div>
</div>

```

We initially have an “anchor”. When clicking the “features” link, the browser will point to this place in the page.

Then we have a bunch of HTML to print the features list.

Include the component in **src/pages/index.astro**:

```

---
import LayoutSite from '@layouts/LayoutSite.astro'
import Hero from '@components/site/homepage/Hero.astro'
import Features from '@components/site/homepage/Features.astro'
---

<LayoutSite>
  <Hero />
  <Screenshot />
  <Features />
</LayoutSite>

```

## Improving the Features component using JavaScript

[&rarr; top](#)

The Features component is a long component, over 100 lines, and most importantly, we have 4 sections that repeat a lot of markup.

If you were to change the color or the size of the text for example, you’d have to change everything in 4 different places.

We can drastically reduce the lines of HTML and fix this problem with one technique, adding a JavaScript array at the top with the values we want to print for the features, and iterating this array inside the HTML.

This is the beauty of Astro components.

We can just write plain HTML, or embed some logic when it helps us.

First we “extract” all the SVG icons to their own component. Create the **src/components/site/homepage/FeaturesIcons** folder and the files:

**Fast.astro**

```

<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
  <path stroke-linecap="round" stroke-linejoin="round" d="m3.75 13.5 10.5-11.25L12 10.5h8.25L9.75 21.75 12 13.5H3.75Z" />
</svg>

```

**Multiplayer.astro**

```

<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
  <path stroke-linecap="round" stroke-linejoin="round" d="M20.25 8.511c.884.284 1.5 1.128 1.5 2.097v4.286c0 1.136-.847 2.1-1.98 2.193-.34.027-.68.052-1.02.072v3.091l-3-3c-1.354 0-2.694-.055-4.02-.163a2.115 2.115 0 0 1-.825-.242m9.345-8.334a2.126 2.126 0 0 0-.476-.095 48.64 48.64 0 0 0-8.048 0c-1.131.094-1.976 1.057-1.976 2.192v4.286c0 .837.46 1.58 1.155 1.951m9.345-8.334V6.637c0-1.621-1.152-3.026-2.76-3.235A48.455 48.455 0 0 0 11.25 3c-2.115 0-4.198.137-6.24.402-1.608.209-2.76 1.614-2.76 3.235v6.226c0 1.621 1.152 3.026 2.76 3.235.577.075 1.157.14 1.74.194V21l4.155-4.155" />
</svg>

```

**Person.astro**

```

<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
  <path stroke-linecap="round" stroke-linejoin="round" d="M15.75 6a3.75 3.75 0 1 1-7.5 0 3.75 3.75 0 0 1 7.5 0ZM4.501 20.118a7.5 7.5 0 0 1 14.998 0A17.933 17.933 0 0 1 12 21.75c-2.676 0-5.216-.584-7.499-1.632Z" />
</svg>

```

**Team.astro**

```

<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
  <path stroke-linecap="round" stroke-linejoin="round" d="M3.75 21h16.5M4.5 3h15M5.25 3v18m13.5-18v18M9 6.75h1.5m-1.5 3h1.5m-1.5 3h1.5m3-6H15m-1.5 3H15m-1.5 3H15M9 21v-3.375c0-.621.504-1.125 1.125-1.125h3.75c.621 0 1.125.504 1.125 1.125V21" />
</svg>

```

Import them all at the top of **src/components/site/homepage/Features.astro**:

```
---
import Person from '@components/site/homepage/FeaturesIcons/Person.astro'
import Team from '@components/site/homepage/FeaturesIcons/Team.astro'
import Fast from '@components/site/homepage/FeaturesIcons/Fast.astro'
import Multiplayer from '@components/site/homepage/FeaturesIcons/Multiplayer.astro'

```

Then we create a **features** array:

```

const features = [



]

```

Inside it we create an object for each feature we want listed in the page:

```

const features = [
  {
    title: 'Solo projects',
    description:
      'The solo plan is perfect for freelancers working on projects on their own',
    icon: Person,
  },
  {
    title: 'Team projects',
    description:
      'The team plan is perfect for small teams working together on multiple projects',
    icon: Team,
  },
  {
    title: 'Fast and easy',
    description:
      'No more overcomplicated project management',
    icon: Fast,
  },
  {
    title: 'Multiplayer mode',
    description: 'Work on projects with your colleagues',
    icon: Multiplayer,
  },
]

```

See, we referenced each icon we imported previously.

Now in the HTML down below we use the syntax:

```

{features.map(feature => (

))}

```

to iterate every item in the **features** array, and inside the parentheses we generate the HTML we want:

```

<div class='px-6 mx-auto mt-32 max-w-7xl sm:mt-56 lg:px-8'>
  <div class='max-w-2xl mx-auto lg:text-center'>
    <h2 class='text-xl font-semibold leading-7'>
      Ship faster
    </h2>
    <p
      class='mt-2 text-3xl font-bold tracking-tight sm:text-5xl'>
      Manage your projects more productively
    </p>
    <p class='mt-6 text-lg leading-8'>
      With its simple interface and useful features,
      SECRETPLAN is the best way to manage your projects.
    </p>
  </div>
  <div
    class='max-w-2xl mx-auto mt-16 sm:mt-20 lg:mt-24 lg:max-w-4xl'>
    <dl
      class='max-w-xl grid grid-cols-1 gap-x-8 gap-y-10 lg:max-w-none lg:grid-cols-2 lg:gap-y-16'>
      {
        features.map(feature => (
          <div class='relative pl-16'>
            <dt class='text-base font-semibold leading-7'>
              <div class='absolute top-0 left-0 flex items-center justify-center w-10 h-10 bg-blue-600 rounded-lg text-white'>
                <feature.icon />
              </div>
              {feature.title}
            </dt>
            <dd class='mt-2 text-base leading-7'>
              {feature.description}
            </dd>
          </div>
        ))
      }
    </dl>
  </div>
</div>

```

You’re beginning to see the true power of Astro components in action.

We use JavaScript, server-side, to create our HTML.

The beauty of this approach is that now to add a new feature in our list we don’t have to write HTML markup - we can add a new item in our array.

And this array can actually be sourced from a database, too, if you want.

If you’re familiar with React, you’ll recognize the syntax is very similar to JSX.

Except it is simpler (no need for **className** for example, or **key** in loops).

Where you see &lt;feature.icon />, notice how we were able to dynamically render a component based on the name included in the **icon** property of the current feature.

Very powerful feature.

## The testimonial(s)

[&rarr; top](#)

Now it’s the turn of the testimonial part. We’ll add a big testimonial in the page.

Create a **src/components/site/homepage/Testimonial.astro** component:

```

<div class="max-w-2xl mx-auto mt-32 sm:mt-56 sm:px-6 lg:px-8">
  <div class="text-center lg:mx-0">
    <blockquote class="mt-6 text-3xl italic font-semibold md:text-6xl">
      “This tool saves me so much time every day.”
    </blockquote>
    <div class="mt-6 text-base">
      <p class="font-semibold">Nelson, CEO of SPRING24APP</p>
    </div>
  </div>
</div>

```

and include it in **src/pages/index.astro**:

```
---
import LayoutSite from '@layouts/LayoutSite.astro'

import Features from '@components/site/homepage/Features.astro'
import Hero from '@components/site/homepage/Hero.astro'
import Testimonial from '@components/site/homepage/Testimonial.astro'
---

<LayoutSite>
  <Hero />
  <Screenshot />
  <Features />
  <Testimonial />
</LayoutSite>

```

Looks pretty nice:

<img class="myMd" src="/image/_image-9a.webp.png" alt="" width=100%>
<!-- ![]('/_image-9a.png') -->

## The pricing section

[&rarr; top](#)

Here is what we’ll have in the pricing section of the homepage:

<img class="myMd" src="/image/_image9AB.webp.png" alt="" width=100%>
<!-- ![]('_image-9AB.webp') -->

As mentioned in the first module, we’ll make the usage of our app free for individuals, and paid for teams.

This will make more people try it, and then maybe decide to purchase it for their team.

So we’ll have a “Create account” button to create a free personal account.

Once you have a personal account you’ll be able to create a team (or more).

Create **src/components/site/homepage/Pricing.astro** and add this HTML markup:

```

<a id='pricing'></a>

<div class='py-24 sm:pt-48'>
  <div class='px-6 mx-auto max-w-7xl lg:px-8'>
    <div class='max-w-4xl mx-auto text-center'>
      <h2 class='text-lg font-semibold leading-7'>
        Pricing
      </h2>
      <p
        class='mt-2 text-4xl font-bold tracking-tight sm:text-5xl'>
        Pricing plans for teams of all sizes
      </p>
    </div>
    <p
      class='max-w-2xl mx-auto mt-6 text-lg leading-8 text-center'>
      The personal plan is free forever
    </p>

    <div
      class='grid max-w-md grid-cols-1 mx-auto mt-10 gap-y-8 sm:mt-10 sm:mx-0 sm:max-w-none sm:grid-cols-2'>
      <div
        class='flex flex-col justify-between p-8 bg-blue-700 border-4 rounded-3xl hover:bg-blue-600 ring-1 ring-gray-200 xl:p-10 sm:mt-8 sm:rounded-r-none'>
        <div>
          <div
            class='flex items-center justify-between gap-x-4'>
            <h3
              id='tier-freelancer'
              class='text-lg font-semibold leading-8 text-white'>
              Personal
            </h3>
          </div>
          <p class='mt-4 text-sm leading-6 text-white'>
            Perfect for individuals and freelancers.
          </p>
          <p class='flex items-baseline mt-6 gap-x-1'>
            <span
              class='text-4xl font-bold tracking-tight text-white'>
              FREE
            </span>
          </p>
          <ul
            role='list'
            class='mt-8 space-y-3 text-sm leading-6 text-white'>
            <li class='flex gap-x-3'>
              <span class='text-white'>✓</span>
              Unlimited projects
            </li>
            <li class='flex gap-x-3'>
              <span class='text-white'>✓</span>
              Unlimited tasks
            </li>
          </ul>
        </div>

        <a
          href='/signup'
          class='block px-3 py-2 mt-8 text-sm font-semibold leading-6 text-center text-white bg-black rounded-md focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-blue-600 ring-1 ring-inset ring-blue-200 hover:ring-blue-300 hover:bg-blue-500'>
          Create account
        </a>
      </div>
      <div
        class='flex flex-col justify-between p-8 bg-black border-4 rounded-3xl hover:bg-zinc-900 ring-1 ring-gray-200 xl:p-10 sm:mt-8 sm:rounded-l-none'>
        <div>
          <div
            class='flex items-center justify-between gap-x-4'>
            <h3
              id='tier-enterprise'
              class='text-lg font-semibold leading-8 text-white'>
              Small Team
            </h3>
          </div>

          <p class='mt-4 text-sm leading-6 text-white'>
            Invite other people and enable collaboration
            tools perfect for small teams.
          </p>

          <p class='flex items-baseline mt-6 gap-x-1'>
            <span
              class='text-4xl font-bold tracking-tight text-white'>
              $25
            </span>
            <span
              class='text-sm font-semibold leading-6 text-white'>
              /month
            </span>
          </p>
          <ul
            role='list'
            class='mt-8 space-y-3 text-sm leading-6 text-white'>
            <li class='flex gap-x-3'>
              <span class='text-white'>✓</span>
              Unlimited projects and tasks
            </li>
            <li class='flex gap-x-3'>
              <span class='text-white'>✓</span> Collaboration
              tools
            </li>
            <li class='flex gap-x-3'>
              <span class='text-white'>✓</span> Up to 10 team
              members
            </li>
          </ul>
          <p class='mt-6 text-sm leading-6 text-white'>
            First create a personal plan, then create a
            team.
          </p>
        </div>
      </div>
    </div>
  </div>
</div>

<div>
  <p class='text-center'>
    More than 10 people in your team? <a
      href='#'
      class='underline'>
      Contact sales
    </a>
  </p>
</div>

```

Include this in **src/pages/index.astro**:

```

---
import LayoutSite from '@layouts/LayoutSite.astro'

import Screenshot from '@components/site/homepage/Screenshot.astro'
import Hero from '@components/site/homepage/Hero.astro'
import Features from '@components/site/homepage/Features.astro'
import Testimonial from '@components/site/homepage/Testimonial.astro'
import Pricing from '@components/site/homepage/Pricing.astro'
---

<LayoutSite>
  <Hero />
  <Screenshot />
  <Features />
  <Testimonial />
  <Pricing />
</LayoutSite>

```

## Frequently asked questions

[&rarr; top](#)

Create **src/components/site/homepage/FAQ.astro**:

```

<div class="max-w-2xl px-6 mx-auto mt-20 text-center lg:max-w-7xl lg:px-8">
  <p class="mt-2 text-4xl font-bold tracking-tight sm:text-5xl">
    Frequently asked questions
  </p>

  <div class="mt-10 space-y-8">
    <div>
      <h2 class="text-lg font-bold">Is the personal account really free?</h2>
      <p class="mt-3">
        Yes! We don’t require a credit card to sign up, it's completely free.
      </p>
    </div>
    <div>
      <h2 class="text-base font-semibold">
        Can I use SPRING24APP for my company?
      </h2>

      <p class="mt-3">
        Absolutely! SPRING24APP is perfect for companies of all sizes.
      </p>
    </div>
  </div>
</div>

```

Note that we have just 2 questions, so I haven’t used a JavaScript array to add them to the HTML like we did for the features component.

But as the number of questions grows, you can definitely create that kind of templating.

Actually it’s a great exercise, please do it. Try to do a similar thing as we did before, but this time, on your own.

Add this component to **src/pages/index.astro**:

```

---
import LayoutSite from '@layouts/LayoutSite.astro'

import Screenshot from '@components/site/homepage/Screenshot.astro'
import Hero from '@components/site/homepage/Hero.astro'
import Features from '@components/site/homepage/Features.astro'
import Testimonial from '@components/site/homepage/Testimonial.astro'
import Pricing from '@components/site/homepage/Pricing.astro'
import FAQ from '@components/site/homepage/FAQ.astro'
---

<LayoutSite>
  <Hero />
  <Screenshot />
  <Features />
  <Testimonial />
  <Pricing />
  <FAQ />
</LayoutSite>

```

<img class="myMd" src="/image/_image9ABC.webp.png" alt="" width=100%>
<!-- ![]('_image-9ABC.png') -->

Note that using this approach you can easily reorder the components on the page by moving them up or down in **index.astro**, so you can experiment with different layouts, for example putting price up or down and measuring the results.

## The footer

[&rarr; top](#)

We’ve reached the footer of the page.

In the footer we’ll add a bunch of links that we’ll later “connect” to pages on our website, pages that we won’t actually create now, but are mostly essential to any product.

This is going to be the result:

<img class="myMd" src="/image/_image-9ABCD.webp.png" alt="-9abcd" width=100%>
<!-- ![]("/_image-9ABCD.webp") -->

See, we have 4 columns that turn into 2 when the screen is small:

<!-- ![]("/_image-9B.webp") -->

<img class="myMd" src="/image/_image-9B.webp.png" alt="9b" width=50%>

This is the HTML we need for this:

```

<div class='max-w-7xl px-6 pb-8 mx-auto mt-20'>
  <footer
    class='py-20 border-t grid grid-cols-2 lg:grid-cols-4 gap-8'>
    <div>
      <h3 class='pb-5 font-semibold leading-6 border-b'>
        Product
      </h3>
      <ul class='mt-6 space-y-4'>
        <li>
          <a
            href='/#features'
            class='leading-6 dark:hover:text-white'
>Features</a
>
        </li>
        <li>
          <a
            href='/#pricing'
            class='leading-6 dark:hover:text-white'
>Pricing</a
>
        </li>
      </ul>
    </div>
    <div>
      <h3 class='pb-5 font-semibold leading-6 border-b'>
        Support
      </h3>
      <ul class='mt-6 space-y-4'>
        <li>
          <a
            href='#'
            class='leading-6 dark:hover:text-white'>
            Documentation
          </a>
        </li>
        <li>
          <a
            href='#'
            class='leading-6 dark:hover:text-white'
>Guides</a
>
        </li>
      </ul>
    </div>
    <div>
      <h3 class='pb-5 font-semibold leading-6 border-b'>
        Company
      </h3>
      <ul class='mt-6 space-y-4'>
        <li>
          <a
            href='#'
            class='leading-6 dark:hover:text-white'
>About</a
>
        </li>
        <li>
          <a
            href='/blog'
            class='leading-6 dark:hover:text-white'
>Blog</a
>
        </li>
      </ul>
    </div>
    <div>
      <h3 class='pb-5 font-semibold leading-6 border-b'>
        Legal
      </h3>
      <ul class='mt-6 space-y-4'>
        <li>
          <a
            href='#'
            class='leading-6 dark:hover:text-white'
>Privacy</a
>
        </li>
        <li>
          <a
            href='#'
            class='leading-6 dark:hover:text-white'
>Terms</a
>
        </li>
      </ul>
    </div>
  </footer>
</div>

```

Again, we can rewrite this HTML to this to avoid the endless repetition of HTML tags that all look the same:

```

---
const columns = [
  {
    title: 'Product',
    rows: [
      { title: 'Features', url: '/#features' },
      { title: 'Pricing', url: '/#pricing' },
    ],
  },
  {
    title: 'Support',
    rows: [
      { title: 'Documentation', url: '#' },
      { title: 'Guides', url: '#' },
    ],
  },
  {
    title: 'Company',
    rows: [
      { title: 'About', url: '#' },
      { title: 'Blog', url: '/blog' },
    ],
  },
  {
    title: 'Legal',
    rows: [
      { title: 'Privacy', url: '#' },
      { title: 'Terms', url: '#' },
    ],
  },
]
---

<div class='max-w-7xl px-6 pb-8 mx-auto mt-20'>
  <footer
    class='py-20 border-t grid grid-cols-2 lg:grid-cols-4 gap-8'>
    {
      columns.map(column => (
        <div>
          <h3 class='pb-5 font-semibold border-b'>
            {column.title}
          </h3>
          <ul class='mt-6 space-y-4'>
            {column.rows.map(row => (
              <li>
                <a
                  href={row.url}
                  class='leading-6 dark:hover:text-white'>
                  {row.title}
                </a>
              </li>
            ))}
          </ul>
        </div>
      ))
    }
  </footer>
</div>

```

Write this in **src/components/site/common/Footer**.astro, and this time include it in the layout, as we’ll share this across all pages in the site:

```

---
import TopBar from '@components/site/common/TopBar.astro'
import Footer from '@components/site/common/Footer.astro'

---

<html lang='en'>
  <head>
    <meta charset='utf-8' />
    <link
      rel='icon'
      type='image/svg+xml'
      href='/favicon.svg'
    />
    <meta name='viewport' content='width=device-width' />
    <title>Secretplan</title>
  </head>
  <body class='dark:bg-black dark:text-white'>
    <div class='max-w-5xl px-4 py-4 mx-auto'>
      <TopBar />
      <slot />
      <Footer />
    </div>
  </body>
</html>

```

## Create the blog

[&rarr; top](#)

Now it’s time to create the product’s blog.

The product blog is where we’ll post updates, sneak peeks, new releases, new features, tips and tricks, case studies, whatever is related to our product / “startup”, maybe also stuff we can post and then promote on social media to get more people to check out our app.

This is what we want to achieve initially, a minimal blog setup that will be available on the **/blog** route:

<img class="myMd" src="/image/_image-9CCD.webp.png" alt="9ccd" width=100%>
<!-- ![]('_image-9CDD.png') -->

And when we click a blog post, we get the single blog post view, corresponding to the URL **/blog/&lt;post-name>**:

<!-- ![]('_image-9CA.png') -->

PENDING

## Create a collection

[&rarr; top](#)

The first thing to do is to create a **content collection**.

A collecation is a super powerful feature of Astro.

It is a way to define a category of content, that we author using **markdowwn**. We can have for example, blog posts, tutorial, changelog or different types of content.

Create a **src/content** folder. Then create **src/content/config.ts** file.

In **contig.ts** file, we define a **blog** collection as follows:

```

import { z, defineCollection } from 'astro:content'

const blog = defineCollection({
  type: 'content',
  schema: z.object({
    title: z.string(),
    date: z.date(),
  }),
})

export const collections = {
  blog,
}

```

We import the **defineCollection** function, and the **z** object, from Astro.

Then we define the **schema** of the collection. Schema is the "structure": title (of type string), and a date (of type **date**).

If the input title is not a string, or the input date is not a date, Astro will display an error.

<img class="myMd" src="/image/_image-9CC.webp" alt="" width=100%>
<!-- ![]('_image-9CC.webp')  -->

Restart the server (ctrl-^) followed by **npm run dev**. Astro needs to see the content of the collection in order to generate the types that Typescript wants to see.

**NOTE**: if you see a red line the command **<code>Developer: Restart Extension Host</code>** may help. If not, restart Astro server.

## Create the blog post list

[&rarr; top](#)

Now create the **blog** folder at **src/content**. The blog posts will have the 'md' extension (markdown).

Let's start with a 'hello world' blog post. Create **src/content/blog/hello-world.md**:

```
---
title: Hello, world!
date: 2024-01-20
---

We did it! aaaa

```

**FRONTMATTER** is the part between **---**.

Below it is the content. **Markdown** is like HTML but much simpler. Start learning the basics, it is worth.

It is time to create the **'route'** that will listen on **/blog**, by creating **src/pages/blog.astro**:

```


---
import LayoutSite from '../layouts/LayoutSite.astro'

import { getCollection } from 'astro:content'
let posts = await getCollection('blog')

posts = posts.sort(
  (a, b) => new Date(b.data.date).valueOf() - new Date(a.data.date).valueOf(),
)
---

<LayoutSite title={'Blog'}>
  <ul class="py-10 px-6 mx-auto max-w-7xl space-y-10">
    {
      posts.map((post) => {
        return (
          <li class="p-8 border rounded-lg">
            <a href={`/blog/${post.slug}/`} class="text-2xl font-bold">
              {post.data.title}
            </a>
          </li>
        )
      })
    }
  </ul>
</LayoutSite>

```

The **imports** are at the top: **getCollection** function from Astro. We call it to get the list of posts using **await getCollection('blog')**.
It an async function. Async function always return a promise. The promise will be either resolved (fullfilled) or rejected at some point in time later. It depends on the network traffic and other factors.

Now the **posts** object contains the array of posts.

We then call the **sort()** method to order posts based on date.

in **blog.astro** file in the markup component we iterate over the posts array to print the list of blog posts.

We pass a **title** prop (a string) to the **LayoutSite** component, so in the LayoutSite.astro **title** field is printed dynamically.

```

---
import TopBar from '@components/site/common/TopBar.astro'
import Footer from '@components/site/common/Footer.astro'

const { title = 'Secretplan' } = Astro.props
---

<html lang='en'>
  <head>
    <meta charset='utf-8' />
    <link rel='icon' type='image/svg+xml' href='/favicon.svg' />
    <meta name='viewport' content='width=device-width' />

    <title>Secretplan</title>
    <title>{title}</title>
  </head>

  <body class='dark:bg-black dark:text-white'>
    <div class='max-w-5xl px-4 py-4 mx-auto'>
      <TopBar />
      <slot />
      <Footer />
    </div>
  </body>
</html>

```

This is the page responsible for showing the list of blog posts.

Now go to http://localhost:4321/blog

<img class="myMd" src="/image/_image-9CCD.webp.png" alt="" width=100%>
<!-- ![]('_image9CCD.png')  -->

## The single blog post view

[&rarr; top](#)

In the previous section we learned how to display all the posts. Now we are going to learn how to display just one post. For that, by clicking on a given post, the web page should be redirected to the content of that post. In order to do that, we need an URL pointing to that specific post. Create the file **src/layouts/MarkdownLayout.astro**. In this file we'll take care of rendering the markdown content of each blog post:

```

---
import LayoutSite from './LayoutSite.astro'

const { title, date } = Astro.props

const formattedDate = (date: string) =>
  new Date(date).toLocaleDateString('en-us', {
    year: 'numeric',
    month: 'short',
    day: 'numeric',
  })
---

<LayoutSite title={title}>
  <div id="markdown" class="py-10 px-6 mx-auto max-w-7xl space-y-10">
    <h1>{title}</h1>
    <p>{formattedDate(date)}</p>
    <hr class="my-4 border-zinc-500" />
    <slot />
  </div>
</LayoutSite>

```

The **MarkdownLayout.astro**'s purpose is just to customize how the blog post is rendered. We could've used the regular **LayoutSite** for that purpose, but then the date would be shown in its defult format. By using a second layout, it allows us to add a **markdown** id attribute to a container **div**, so we can later style the markdown with CSS. SUPERIMPORTANT!!!

Now, let's create a dynamic route (URL) to render one post. Create **src/pages/blog/[slug].astro**.

Each blog post's file title will determine the website page route (URL). For instance, **hello-world.md** turns into **src/pages/blog/hello-world**.

You don't need to create a route for each blog post (remember Reddit web site? the **/r/something route**?). The **[slug].astro** takes care of the dynamic part.

in **[slug].astro** file we add:

```

---
import MarkdownLayout from '@layouts/MarkdownLayout.astro'
import { getCollection } from 'astro:content'

export async function getStaticPaths() {
  let posts = await getCollection('blog')

  return posts.map((post) => ({
    params: { slug: post.slug },
    props: { post },
  }))
}

const { post } = Astro.props
const { Content } = await post.render()
---

<MarkdownLayout title={post.data.title} date={post.data.date}>
  <Content />
</MarkdownLayout>

```

Basically Astro at build time will generate the blog posts from our blog collection.

Notice how we use the MarkdownLayout component we’ve previously created, passing it the title and the date, which is then used in src/layouts/MarkdownLayout.astro.

Awesome!

Things work, but our blog posts look a bit boring: everything looks the same, the title is not big enough, the list is not rendered as a list…

<img class="myMd" src="/image/_image-9D.png" alt="-9d" width=100%>
<!-- ![]('/_image-9D.png') -->

We can add some CSS to style our blog posts, and here’s how the markdown id we added to MarkdownLayout.astro will prove to be useful.

Create a **src/site.css** file:

```

@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  #markdown {
    @apply text-black dark:text-white;
  }
  #markdown h1 {
    @apply text-4xl font-extrabold tracking-tight mt-0;
  }

  #markdown h2 {
    @apply text-3xl font-extrabold tracking-tight mt-10;
  }

  #markdown h3 {
    @apply text-2xl font-extrabold tracking-tight mt-10;
  }

  #markdown h4 {
    @apply mt-4 text-gray-500 mb-4;
  }

  #markdown p {
    @apply mt-4;
  }

  #markdown ul,
  #markdown ol {
    @apply mt-2  list-inside;
  }
  #markdown ul {
    @apply list-disc;
  }
  #markdown ol {
    @apply list-decimal;
  }
  #markdown li {
    @apply pt-2;
  }

  #markdown img {
    @apply dark:invert;
  }
}

```

Now import it in the LayoutSite.astro to load the CSS:

```

---
import TopBar from '@components/site/common/TopBar.astro'
import Footer from '@components/site/common/Footer.astro'

import '@src/site.css'

const { title = 'Secretplan' } = Astro.props
---
```

<img class="myMd" src="/image/_image-9D20.png" alt="" width=100%>
<!-- ![]('/_image-9D20.png') -->

## List the latest blog post in the homepage

[&rarr; top](#)

One thing I want to do is showing the latest blog post in the homepage.

It’s nice to show visitors the latest news.

We’ll do that in src/components/site/homepage/Hero.astro.

First we add a section to gather the posts from the blog collection, and order them by date:

```

---
import { getCollection } from 'astro:content'
let posts = await getCollection('blog')

posts = posts.sort(
  (a, b) =>
    new Date(b.data.date).valueOf() -
    new Date(a.data.date).valueOf()
)
---

```

Then we add the latest blog post data to the HTML by referencing posts[0] (the first blog post in the list, now ordered from most recent to oldest):

```

    </p>

    <div class='mx-auto mb-10'>
      <a
        href={`/blog/${posts[0].slug}`}
        class='px-4 py-2 text-sm rounded-full bg-zinc-800 text-zinc-200 font-semibold'>
        New: {posts[0].data.title} &rarr;
      </a>
    </div>

    <h1
      class='text-4xl font-bold tracking-tight sm:text-6xl'>
      The easiest way to manage your projects
    </h1>

```

Use as a reference the **<code><h1></code> tag** to add the code snippet in the correct place.

Here it is:
<img class="myMd" src="/image/_image-9D22.png" alt="9d22" width=100%>

<!-- ![]('/_image-9D22.png') -->

The logo needs to be fixed. I'll do it at a later date.

## Wrapping module 2

[&rarr; top](#)

We did it!

We build a pretty cool site with a homepage built using a component-based approach.

We used content collections to create a blog.

The site works on mobile or desktop, looks nice in light or dark mode.

The website is statically pre-rendered at build time.

What does this mean? Basically, when you deploy the site, Astro generates the HTML, and that’s it.

In the next modules we’ll add Server-Side Rendering (SSR) in order to make our application dynamic, but what you’ve built so far is a static site that can be deployed on a simple hosting platform like Netlify or Cloudflare Pages without any more work to do.

## Troubleshooting

[&rarr; top](#)

Sometimes I run into issues in VS Code when working in my Astro projects, I don’t know it it’s VS Code, TypeScript, Astro, more likely a combination of it all.

Sometimes errors are subtle / confusing, for example in one case I create a file and imported it, but I got a red line under the import saying Cannot find module ... or its corresponding type declarations

You can try opening the VS Code command palette and execute Developer: Restart Extension Host or Developer: Reload Window and more often than not, the error goes away.

Also try stopping npm run dev and restarting it.

Final try, close VS Code and reopen it.

Sometimes the issue is that Types were not generated. If you click on "quick fix" if available it may solve the issue. Note that VS Code will add some code defining the types. Check your code for any changes.

Running **\*npx astro sync** may work. If nothing works, ask for help.

## Source code

[&rarr; top](#)

I will provide the full code of this module at the beginning of our next week (week 5 in our quarter). Also, I will provide the full code each week toward the end of the week depending our progress.

### This was the content of this module:

1. [Introduction](#introduction)
1. [Goals](#goals)
1. [What is Astro](#what-is-astro)
1. [Installing Astro locally](#installing-astro-locally)
1. [Install Astro](#install-astro)
1. [Creating folder structure manually](#creating-folder-structure-manually)
1. [Create first Astro page](#create-your-first-page)
1. [Create first static asset](#create-first-static-asset)
1. [Edit astro config mjs file](#edit-astroconfigmjs-file)
1. [Adding TypeScript support](#adding-typescript-support)
1. [Starting Astro application](#starting-astro-application)
1. [Configuring VS Code Prettier extension](#configuring-vs-code-prettier-extension)
1. [About TypeScript](#about-typescript)
1. [Overview of starter Astro site](#overview-of-starter-astro-site)
1. [Astro vs other JS frameworks](#astro-vs-other-js-frameworks)
1. [Astro Homepage](#astro-homepage)
1. [Light mode](#in-light-mode)
1. [Dark mode](#in-dark-mode)
1. [In mobile device](#here-the-view-in-a-mobile-device)
1. [Manual install Astro Tailwind extension](#manual-install-astro-tailwind-extension)
1. [Manual install NodeJS integration](#manual-install-nodejs-integration)
1. [Instal dotenv module](#install-dotenv-module)
1. [Create a layout](#create-a-layout)
1. [Tips from Flavio Copes](#tips-from-flavio-copes)
1. [Module2 part B](#module-2-part-b)
1. [We created a simple layout page]
1. [The top bar](#the-top-bar)
1. [Dark mode](#dark-mode)
1. [The hero section](#the-hero-section)
1. [Screenshot of the app in action](#the-screenshot-of-the-app-in-action)
1. [The feature list](#the-feature-list)
1. [Improving the Feature component using JavaScript](#improving-the-features-component-using-javascript)
1. [Testimonials](#the-testimonials)
1. [The pricing section](#the-pricing-section)
1. [Frequently asked questions](#frequently-asked-questions)
1. [The footer](#the-footer)
1. [Create the blog](#create-the-blog)
1. [Create a collection](#create-a-collection)
1. [Create the blog post list](#create-the-blog-post-list)
1. [The single blog post view](#list-the-latest-blog-post-in-the-homepage)
1. [Wrapping module 2](#wrapping-module-2)
1. [Troubleshooting](#troubleshooting)
