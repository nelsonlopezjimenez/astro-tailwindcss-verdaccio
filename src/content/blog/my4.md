---
title: Module 4
date: 2024-01-20
---

# content

1. [content](#content)
1. [Module 4](#module-4)
1. [The Internet](#the-internet)
1. [The Web](#the-web)




## The Internet

asdfsad adsf sdf sdf sdf dsfdf



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

## Module 4

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
# !!!QW


<img class="myMd" src="../_image(48).png" alt="_image(48)" width=100%/>

<img class="myMd" src="/_image(48).png" alt="_image(48)" width=100% />

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

## The Web

Now write “Top Bar” in the TopBar.astro component, and it will
appear in the website:


<img class="myMd" src="../topbar-astro_image.webp" alt="topbar-astro_image.webp" width=100%>
<img class="myMd" src="/topbar-astro_image.webp" alt="topbar-astro_image.webp" width=100%>

The logo1 is in the public folder of the Astro site:


Anything in the public folder is statically served from Astro, this means you can access it using as http://localhost:4321/logo1.svg.