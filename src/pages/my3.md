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


<img src="../src-compnts-site-common-homepage_image.webp" alt="topbar-astro_image.webp" width=100%/>

<img src="/src-compnts-site-common-homepage_image.webp" alt="topbar-astro_image.webp" width=100% />

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


<img src="../topbar-astro_image.webp" alt="topbar-astro_image.webp" width=100%>
<img src="/topbar-astro_image.webp" alt="topbar-astro_image.webp" width=100%>

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

<img src="../secretplan-svg-navflexmenu.webp" alt="secretplan-svg-navlfexmenu.webp" width=100%>
<img src="/secretplan-svg-navflexmenu.webp" alt="secretplan-svg-navlfexmenu.webp" width=100%>


## Dark mode issues

If you use dark mode in your OS you don’t see the logo, because the logo is white. In light mode we invert it to black using the invert class, but we revert the invert in dark mode using **dark:invert-0.**

<!-- ![]('/public/_image-4.webp') -->
<img src="../_image-4.webp" alt="_image-4.webp" width=100%>
<img src="/_image-4.webp" alt="/_image-4.webp" width=100%>

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

<img src="../_image-5.webp" alt="_image-5.webp" width=100%>
<img src="/_image-5.webp" alt="/_image-5.webp" width=100%>
<!-- ![]('/_image-5.webp') -->

We also set some padding on an inner div, the max width with max-w-5xl, and mx-auto to center this into the page.

I highly encourage you to search on the Tailwind CSS official documentation what those classes do. I do this all the time for classes I don’t remember.

## The hero section


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

<img src="../_image-6.webp" alt="6" width=100%>
<img src="/_image-6.webp" alt="6" width=100%>
<!-- ![]('/_image-6.webp') -->

## The screenshot of the app  in action

Let’s now add a big screenshot of the app in action. We haven’t built the app yet, but suppose we have the designs our designer provided us.

Use this screenshot image:

<!-- ![]('/head-after-pic1a.png') -->
<img src="../head-after-pic1a.png" alt="pic1a" width=100%>
<img src="/head-after-pic1a.png" alt="/pic1a" width=100%>

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

<img src="../_image-7.webp" alt="" width=100%>
<img src="/_image-7.webp" alt="" width=100%>
<!-- ![]('/_image-7.webp.png') -->

## The feature list

Let’s now add the features list.

This is the end result we want:

<img src="../_image-7.webp.png" alt="" width=100%>
<img src="/_image-7.webp.png" alt="" width=100%>
<!-- ![]('/_image-7.png') -->


When the screen gets smaller:

<img src="../_image-9.webp" alt="" width=100%>
<img src="/_image-9.webp" alt="" width=100%>
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

<img src="../_image-9a.webp.png" alt="" width=100%>
<img src="/_image-9a.webp.png" alt="" width=100%>
<!-- ![]('/_image-9a.png') -->

## The pricing section

Here is what we’ll have in the pricing section of the homepage:

<img src="../_image9AB.webp" alt="" width=100%>
<img src="/_image9AB.webp" alt="" width=100%>
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

<img src="../_image9ABC.webp.png" alt="" width=100%>
<img src="/_image9ABC.webp.png" alt="" width=100%>
<!-- ![]('_image-9ABC.png') -->


Note that using this approach you can easily reorder the components on the page by moving them up or down in **index.astro**, so you can experiment with different layouts, for example putting price up or down and measuring the results.

## The footer

We’ve reached the footer of the page.

In the footer we’ll add a bunch of links that we’ll later “connect” to pages on our website, pages that we won’t actually create now, but are mostly essential to any product.

This is going to be the result:

<img src="../_image-9ABCD.webp" alt="" width=100%>
<img src="/_image9-ABCD.webp" alt="" width=100%>
<!-- ![]("/_image-9ABCD.webp") -->

See, we have 4 columns that turn into 2 when the screen is small:

<!-- ![]("/_image-9B.webp") -->
<img src="../_image-9B.webp" alt="" width=50%>
<img src="/_image-9B.webp" alt="" width=50%>

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

Now it’s time to create the product’s blog.

The product blog is where we’ll post updates, sneak peeks, new releases, new features, tips and tricks, case studies, whatever is related to our product / “startup”, maybe also stuff we can post and then promote on social media to get more people to check out our app.

This is what we want to achieve initially, a minimal blog setup that will be available on the **/blog** route:

<img src="../_image-9CCD.webp" alt="" width=100%>
<img src="/_image-9CCD.webp" alt="" width=100%>
<!-- ![]('_image-9CDD.png') -->

And when we click a blog post, we get the single blog post view, corresponding to the URL **/blog/&lt;post-name>**:

<!-- ![]('_image-9CA.png') -->


PENDING
## Create a collection

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

<img src="../_image-9CC.webp" alt="" width=100%>
<img src="/_image-9CC.webp" alt="" width=100%>
<!-- ![]('_image-9CC.webp')  -->

Restart the server (ctrl-^) followed by **npm run dev**. Astro needs to see the content of the collection in order to generate the types that Typescript wants to see.

**NOTE**: if you see a red line the command **<code>Developer: Restart Extension Host</code>** may help. If not, restart Astro server.

## Create the blog plost list

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

<img src="../_image-9CCD.webp.png" alt="" width=100%>
<img src="/_image-9CCD.webp.png" alt="" width=100%>
<!-- ![]('_image9CCD.png')  -->

## The single blog post view

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

<img src="../_image-9D.png" alt="" width=100%>
<img src="/_image-9D.png" alt="" width=100%>
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

<img src="../_image-9D20.png" alt="" width=100%>
<img src="/_image-9D20.png" alt="" width=100%>
<!-- ![]('/_image-9D20.png') -->

## List the latest blog post in the homepage

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

<img src="../_image-9D22.png" alt="" width=100%>
<img src="/_image-9D22.png" alt="" width=100%>
<!-- ![]('/_image-9D22.png') -->


The logo needs to be fixed. I'll do it at a later date.

## Wrapping the module 2

We did it!

We build a pretty cool site with a homepage built using a component-based approach.

We used content collections to create a blog.

The site works on mobile or desktop, looks nice in light or dark mode.

The website is statically pre-rendered at build time.

What does this mean? Basically, when you deploy the site, Astro generates the HTML, and that’s it.

In the next modules we’ll add Server-Side Rendering (SSR) in order to make our application dynamic, but what you’ve built so far is a static site that can be deployed on a simple hosting platform like Netlify or Cloudflare Pages without any more work to do.

## Troubleshooting 

Sometimes I run into issues in VS Code when working in my Astro projects, I don’t know it it’s VS Code, TypeScript, Astro, more likely a combination of it all.

Sometimes errors are subtle / confusing, for example in one case I create a file and imported it, but I got a red line under the import saying Cannot find module ... or its corresponding type declarations

You can try opening the VS Code command palette and execute Developer: Restart Extension Host or Developer: Reload Window and more often than not, the error goes away.

Also try stopping npm run dev and restarting it.

Final try, close VS Code and reopen it.

Sometimes the issue is that Types were not generated. If you click on "quick fix" if available it may solve the issue. Note that VS Code will add some code defining the types. Check your code for any changes.

Running ***npx astro sync** may work. If nothing works, ask for help.

## Source code

I will provide the full code of this module at the beginning of our next week (week 5 in our quarter). Also, I will provide the full code each week toward the end of the week depending our progress.


### This was the content of this module:

1:	Introduction to the module
2:	Introducing Astro
3:	Using Astro via StackBlitz
4:	Installing Astro locally
5:	A note on configuration
6:	About TypeScript
7:	Overview of the starter Astro site
8:	Astro vs other JS frameworks
9:	Let’s start with the homepage
10:	Install the Astro Tailwind extension
11:	Create a layout
12:	The top bar
13:	Dark mode issues
14:	The hero section
15:	The screenshot of the app in action
16:	The features list
17:	Improving the Features component using JavaScript
18:	The testimonial(s)
19:	The pricing section
20:	Frequently asked questions
21:	The footer
22:	Create the blog
23:	Create a collection
24:	Create the blog posts list
25:	The single blog post view
26:	List the latest blog post in the homepage
27:	Wrapping up module 2
28:	Push your code to GitHub
29:	Troubleshooting
30:	Source code

