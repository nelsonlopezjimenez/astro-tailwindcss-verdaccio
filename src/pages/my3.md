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
Create a components folder in src .
Inside it we’re going to have a lot of components, so we’d better
think about organizing them nicely.
Our Astro site will handle both the public-facing site, and the
web app part, so the first big organization is to separate them
into site and app components.
Inside src/components/site we can further organize by creating a
common folder to host components reused across all the website
(like the top bar component) and a homepage folder that will host only components related to the homepage, our most complicated
page.

Inside common create the file TopBar.astro .
Import it in LayoutSite.astro , and include it right before the
&lt;slot />:

```

---
import TopBar from '@components/site/common/TopBar.astro'
---
<html lang='en'>
<head>
    <meta charset='utf-8' />
    <link rel='icon' type='image/svg+xml' href='/favicon.svg'
    />
    <meta name='viewport' content='width=device-width' />
    <title>Spring24app</title>
</head>
<body>
    <TopBar />
    <slot />
</body>
</html>

```

Now write “Top Bar” in the TopBar.astro component, and it will
appear in the website.

# Tips from Flavio Copes

💁‍♂️ TIP: Tailwind is called a “utility framework”. If you already know another framework like Bootstrap, Tailwind is similar but kind of different. Instead of providing you with more CSS classes, like .container or .btn-primary that do not tell you exactly what they do, you have what it’s called utility classes. Like .text-right or .text-left. They tell you precisely what they do. And they just do one thing. In this case, they move the text to the right or left. This is just an example. There are many more of those classes, each applying a single property of CSS rather than many at once as happens with Bootstrap.

```

```
