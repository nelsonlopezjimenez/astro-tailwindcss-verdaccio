# Module 2a - week 4.17 (cont)

We created a Astro-based website. It consists of homepage, and some other pages (layout pages). We installed Tailwind, Tailwindcss, integration to node, and manually edited configuration files.
we discussed Astro versus other JavaScript frameworks.

We'll be using Tailwind to build a layout that is responsive and handles dark and bright mode. We'll learn how to use Astro components to compose the HTML, server side, using JavaScript imports. Also, we'll learn how to create dynamic routes and how to use content collections to build the app.

## Contents

1. We created a simple layout page
1. The top bar
1. Dark mode
1. The hero section
1. The feature list
1. Improving the Feature component using JavaScript
1. The pricing section
1. Frequently asked questions
1. The footer
1. Create the blog
1. Create a collection
1. Create the blog post list
1. The single blog post view
1. Wrapping module 2

## Previously...

At the end of the previous document you imported the first component into src/pages/index.astro file as follows:

```

import LayoutSite from '@layouts/LayoutSite.astro';

<LayoutSite>
    <h1>Astro</h1>
</LayoutSite>

```

## The top bar

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

![]('src-compnts-site-common-homepage_image.webp')

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

![]('/topbar-astro_image.webp')

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


The links point to locations we’ll create later on. In particular, /login and /blog are different pages (we’ll build blog later in this module). /#pricing and /#features will be locations in the homepage where people can find information about (guess what) the features and the pricing.

An important class we use, that determines how the whole component looks like, is **flex**. This enables flexbox on the <nav> tag.

justify-between equally separates the 3 children of nav.

The flex-1 class on the first and last makes sure they expand to equally take the space remaining, so one stays left, one right.

The middle part, we only show it when the screen is large enough, using hidden md:flex.

Then the each individual link is separated from each other using gap-x-12.

This is the result:



# Tips from Flavio Copes

💁‍♂️ TIP: Tailwind is called a “utility framework”. If you already know another framework like Bootstrap, Tailwind is similar but kind of different. Instead of providing you with more CSS classes, like .container or .btn-primary that do not tell you exactly what they do, you have what it’s called utility classes. Like .text-right or .text-left. They tell you precisely what they do. And they just do one thing. In this case, they move the text to the right or left. This is just an example. There are many more of those classes, each applying a single property of CSS rather than many at once as happens with Bootstrap.

```

```
