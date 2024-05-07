---
title: Module 3
date: 5/3/2024
---

We build a pretty cool site with a homepage built using a component-based approach.

We used content collections to create a blog.

The site works on mobile or desktop, looks nice in light or dark mode.

The website is statically pre-rendered at build time.

What does this mean? Basically, when you deploy the site, Astro generates the HTML, and that’s it.

In the this and following modules we’ll add Server-Side Rendering (SSR) in order to make our application dynamic, but what you’ve built so far is a static site that can be deployed on a simple hosting platform like Netlify or Cloudflare Pages without any more work to do.

## Content

1. [Introduction to the module](#introduction)
2. [Create a dashboard](#create-a-dashboard)
3. [Start fetching data from PocketBase](#start-fetching-data-from-pocketbase)
4. [Show the projects list on the page](#show-the-projects-list-on-the-page)
5. [Create a layout for the app](#create-a-layout-for-the-app)
6. [Show projects nicely](#show-projects-nicely)
7. [Show the project status](#show-the-project-status)
8. [The problem we’re facing with static site rendering](#the-problem-we-are-facing-with-static-rendering)
9. [Enable SSR mode in Astro](#enable-ssr-server-side-rendering-mode-in-astro)
10. [SSR vs SSG mode](#ssr-vs-ssg-mode)
11. [Add a way to create a new project from the app](#add-a-way-to-create-a-new-project-from-the-app)
12. [Create a modal container](#create-a-modal-container)
13. [Time to introduce htmx](#what-is-htmx)
14. [Show the modal](#show-the-modal)
15. [Add the form to the modal](#add-the-form-to-the-modal)
16. [Close the modal when we click outside of it](#close-the-modal-when-we-click-outside-of-it)
17. [Create the new project](#create-the-new-project)
18. [Create the single project page](#create-the-single-project-page)
19. [Add a way to add tasks to a project](#add-a-way-to-add-tasks-to-a-project)
20. [List the project tasks](#list-the-project-tasks)
21. [Troubleshooting](#troubleshooting)
22. [Wrapping up](#wrapping-up)

# Introduction

[&rarr; top](#)

In module 1, we talked about what the app will do, we defined the data model, we installed PocketBase, explored it, and then we created the projects and tasks collections to store our app data.

In module 2 we started working with Astro and we created the “site” part of the project.

In this module, module 3, we’ll start working on the “app” part:

1. we’ll create a dashboard
1. we’ll start fetching data from PocketBase
1. we’ll show the projects list
1. we’ll add a way to create a new project
1. we’ll add a way to add tasks to a project and we’ll list those tasks
1. we’ll introduce htmx and I’ll show you how to use it to perform actions

## Create a dashboard

[&rarr; top](#)

Create the folder **src/pages/app** and inside it create the file **dashboard.astro**

Now visit the URL **http://localhost:4321/app/dashboard**.

You'll see a blank page.

<!-- <img src="../_image3MA.webp" alt="image3MA" width=70% /> -->
<img src="/image/_image3MA.webp" alt="image3MA" width=70% />

In Astro, if there’s no page route corresponding to a URL, you’ll see a “404 not found” page:

<!-- <img src="../_image3MB.webp" alt="image3MA" width=70% /> -->
<img src="/image/_image3MB.webp" alt="image3MA" width=70% />

404 is the HTTP response status code for “page not found”. The HTTP server returns this status code to the client.

You can see the HTTP response status code in the **DevTools Network panel**:

<!-- <img src="../_image3MC.webp" alt="image3MA" width=70% /> -->
<img src="/image/_image3MC.webp" alt="image3MA" width=70% />

<!-- <img src="../_image3MD.webp" alt="image3MA" width=70% /> -->
<img src="/image/_image3MD.webp" alt="image3MA" width=70% />

A successful response has status code 200.

What we want to do is start the whole “app part” by listing all the projects in the projects collection in PocketBase.

Go to the PocketBase “Admin UI” URL **http://127.0.0.1:8090/_/**, as we’ve done in Module 1 (restart PocketBase if you stopped its process with **./pocketbase serve** (**.\pocketbase serve** on Windows Powershell) from the folder where you added the PocketBase command, as we did in module 1).

Here is the projects collection we created in module 1:

<!-- <img src="../_image3ME.webp" alt="image3MA" width=70% /> -->
<img src="/image/_image3ME.webp" alt="image3MA" width=70% />

I want to add some projects here, using the PocketBase interface.

But first we have to add a user. The reason is that each product has a created_by property that links to a user.

So first go to the users collection and add a user by clicking “New record”:

<!-- <img src="../_image3MF.webp" alt="image3MA" width=70% /> -->
<img src="/image/_image3MF.webp" alt="image3MA" width=70% />

You’ll see a form show up:

<!-- <img src="../_image3MG.webp" alt="image3MA" width=70% /> -->
<img src="/image/_image3MG.webp" alt="image3MA" width=70% />

Fill the Email and Password fields. Also set Public: On on the email field (see the green text in the screenshot below) — we’ll talk about this later, but basically we’ll use this to be able to search users by email, by default unlocked for privacy reasons.

<!-- <img src="../_image3MH.webp" alt="image3MA" width=70% /> -->
<img src="/image/_image3MH.webp" alt="image3MA" width=70% />

Click “Create” and you should see the record:

<!-- <img src="../_image3MI.webp" alt="image3MA" width=70% /> -->
<img src="/image/_image3MI.webp" alt="image3MA" width=70% />

Now select to the projects collection.

Click “New record” and add a few sample projects:

<!-- <img src="../_image3MJ.webp" alt="image3MA" width=70% /> -->
<img src="/image/_image3MJ.webp" alt="image3MA" width=70% />

Set a name, a status from the list, and pick a user:

<!-- <img src="../_image3MK.webp" alt="image3MA" width=70% /> -->
<img src="/image/_image3MK.webp" alt="image3MA" width=70% />

Add a few records, just to have some data to visualize:

<!-- <img src="../_image3ML.webp" alt="image3MA" width=70% /> -->
<img src="/image/_image3ML.webp" alt="image3MA" width=70% />

## Start fetching data from PocketBase

[&rarr; top](#)

Now we’re ready to fetch the data from PocketBase.

To do this, go to the terminal and install the pocketbase npm package.

This is the first npm package we install. This is how we “import” code that other people created, and we can use in our projects.

Run the command from the folder that contains package.json (the root folder of Astro):

```

npm install pocketbase@0.21.1

```

<!-- <img src="../_image3MM.webp" alt="image3MA" width=70% /> -->
<img src="/image/_image3MM.webp" alt="image3MA" width=70% />

The entry has been added to the package.json file:

<!-- <img src="../_image3MN.webp" alt="image3MA" width=70% /> -->
<img src="/image/_image3MN.webp" alt="image3MA" width=70% />

(your exact version numbers will change but don’t worry)

Now in src/pages/app/dashboard.astro add this code:

```

---
import PocketBase from 'pocketbase'

const pb = new PocketBase('http://127.0.0.1:8090')

const projects = await pb
  .collection('projects')
  .getFullList()

console.log(projects)
---

```

Reload the dashboard, now in the terminal you should see the output of the console.log() - remember, anything we write in the “frontmatter” of an Astro component (the part between the --- lines) is ran server-side, so we don’t see the output in the browser console, but rather in the terminal where npm run dev is running.

You should see all the projects data printed:

<!-- <img src="../_image3MO.webp" alt="image3MA" width=70% /> -->
<img src="/image/_image3MO.webp" alt="image3MA" width=70% />

## Show the projects list on the page

[&rarr; top](#)

The dashboard is still an empty page.

In the dashboard.astro page component now we can iterate the projects array, similarly to how we iterated over arrays when we built the homepage to show features or the footer:

```

---
import PocketBase from 'pocketbase'

const pb = new PocketBase('http://127.0.0.1:8090')

const projects = await pb.collection('projects').getFullList()
---

<ul>
  {projects.map(project => <li>{project.name}</li>)}
</ul>

```

Here is the result:

<!-- <img src="../_image3MP.webp" alt="image3MA" width=70% /> -->
<img src="/image/_image3MP.webp" alt="image3MA" width=70% />

## Create a layout for the app

This method we used to show the projects list is ok, but let’s do it in a different way now.

We’re going to create a lot of screens in the “app” portion of our project, so let’s create a src/layouts/LayoutApp.astro layout - similarly to what we did with src/layouts/LayoutSite.astro for the site part.

```

---
const { title = 'Spring24app' } = Astro.props
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
    <title>{title}</title>
    <meta
      name='description'
      content='A project management tool'
    />
  </head>

  <body>
    <main class='min-h-screen dark:bg-black dark:text-white'>
      <div class='max-w-5xl px-4 py-4 mx-auto'>
        <slot />
      </div>
    </main>
  </body>
</html>

```

This layout has a title prop, that will be used to fill the &lt;title> tag content.

Any page that uses this layout can pass the title information as a prop, like this:

```

<LayoutApp title='Dashboard'>
  ...
</LayoutApp>

```

That’s what we’re going to do in src/pages/app/dashboard.astro:

```

---
import PocketBase from 'pocketbase'

import LayoutApp from '@layouts/LayoutApp.astro'

const pb = new PocketBase('http://127.0.0.1:8090')

const projects = await pb
  .collection('projects')
  .getFullList()
---

<LayoutApp title='Dashboard'>
  <ul>
    {projects.map(project =>
      <li>{project.name}</li>
    )}
  </ul>
</LayoutApp>

```

**TIP** Sometimes you may get an error when adding a file to VS Code and then import it. Running **Developer: Restart Extension Host** command in VS Code from the Command Palette (cmd-shift-p OR ctrl-shift-p OR shift-greaterthan key).

The layout now provides some built-in padding that will be set across all pages in our app:

<!-- <img src="../_image3MQ.webp" alt="image3MA" width=70% /> -->
<img src="/image/_image3MQ.webp" alt="image3MA" width=70% />

## Show projects nicely

[&rarr; top](#)

Now I’m going to create a ProjectCard component that will be responsible for showing a single project in our list.

Create the file src/components/app/projects/ProjectCard.astro and inside it we’re going to start simple.

VS Code tip: you can right click after all the files list in the root of the project, select “New File…”, then paste that whole string including / in the root of the project VS Code will auto-create all folders, pretty handy

We get the project object as a prop, and we print the project name in a &lt;li> tag:

```

---
const { project } = Astro.props
---

<li>
  {project.name}
</li>

```

In src/pages/app/dashboard.astro we import this component and we use it in our projects.map() iteration:

```

---

import PocketBase from 'pocketbase'
import LayoutApp from '@layouts/LayoutApp.astro'
import ProjectCard from '@components/app/projects/ProjectCard.astro'

const pb = new PocketBase('http://127.0.0.1:8090')

const projects = await pb
.collection('projects')
.getFullList()

---

<LayoutApp title='Dashboard'>
  <ul>
    {projects.map(project =>
      <li>{project.name}</li> REPLACE THIS LINE BY THE NEXT!!!
      <ProjectCard project={project} />
    )}
  </ul>
</LayoutApp>

```

Everything should work exactly as before.

But now we can work in the ProjectCard component to make things look prettier:

```

---
const { project } = Astro.props
---

<li>      DELETE THIS LINE
  {project.name}  DELETE THIS LINE
</li>   DELETE THIS LINE
<li
  class='text-zinc-800 dark:text-white border dark:border-none rounded-lg bg-zinc-100 dark:bg-zinc-800 hover:bg-zinc-200 hover:dark:bg-zinc-700'>
  <a href={`/app/project/${project.id}`}>
    <div
      class='flex justify-center w-full p-6'>
      <h3
        class='text-lg font-bold truncate'>
        {project.name}
      </h3>
    </div>
  </a>
</li>

```

This adds some padding to each project, and also links to the project detail page when each card is clicked:

<!-- <img src="../_image3MR.png" alt="image3MR" width=70% /> -->

<img src="/image/_image3MR.png" alt="image3MR" width=70% />

Now in src/pages/app/dashboard.astro we can wrap our cards in a container with grid grid-cols-2 to display 2 projects on each row (only on big screens), and we’re also applying a gap to visually separate them:

```

<LayoutApp title='Dashboard'>
  <div class='py-10 mx-auto text-white max-w-7xl'>
      <ul>
      <ul class='grid gap-6 sm:grid-cols-2'>
        {
          projects.map(project => (
            <ProjectCard project={project} />
          ))
        }
      </ul>
  </div>
</LayoutApp>

```

<!-- <img src="../_image3MS.png" alt="image3MS" width=70% /> -->

<img src="/image/_image3MS.png" alt="image3MS" width=70% />

On small screens you’ll get 1 column, thanks to using sm: before grid-cols-2 in our Tailwind CSS class:

<!-- <img src="../_image3MT.png" alt="image3MT" width=70% /> -->

<img src="/image/_image3MT.png" alt="image3MT" width=70% />

Let’s also add a title so users knows what they’re looking at:

```

<LayoutApp title='Dashboard'>
   <div class='py-10 mx-auto text-white max-w-7xl'>
   <div class='py-10 mx-auto text-white max-w-7xl space-y-6'>
   <div
     class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 text-xl sm:text-3xl md:text-5xl text-white uppercase text-center font-extrabold'>
     Projects
   </div>


    <ul class='grid gap-6 sm:grid-cols-2'>
      {
        projects.map(project => (
          <ProjectCard project={project} />
        ))
      }
    </ul>
  </div>
</LayoutApp>

```

Pretty nice:

<!-- <img src="../_image3MU.png" alt="image3MU" width=70% /> -->

<img src="/image/_image3MU.png" alt="image3MU" width=70% />

## Show the project status

[&rarr; top](#)

Now let’s display each project’s status in the project card.

Remember, we have the status information that stores the current project state, for example “not started” or “in progress” or “completed”:

<!-- <img src="../_image3MV.png" alt="image3MV" width=70% /> -->

<img src="/image/_image3MV.png" alt="image3MV" width=70% />

Here’s what we want to achieve:

<!-- <img src="../_image3MW.png" alt="image3MW" width=70% /> -->

<img src="/image/_image3MW.png" alt="image3MW" width=70% />

To do this, first we add some markup to the card HTML in src/components/app/projects/ProjectCard.astro:

```

<li
  class='text-zinc-800 dark:text-white border dark:border-none rounded-lg bg-zinc-100 dark:bg-zinc-800 hover:bg-zinc-200 hover:dark:bg-zinc-700'>
  <a href={`/app/project/${project.id}`}>
    <div
      class='flex justify-center w-full p-6'>
      <h3
        class='text-lg font-bold truncate'>
        {project.name}
      </h3>
    </div>

    <div
      class={`bg-zinc-100 dark:bg-zinc-800 rounded-b-lg text-center border-t ${
        project.status !== 'not started' &&
        project.status !== 'ongoing' &&
        project.status !== 'on hold' &&
        project.status !== 'done' &&
        'border-t-blue-600 dashed-border-top'
      }`}>
      <div
        class="inline-block px-1 mt-[0.35rem] text-sm text-zinc-900 bg-zinc-100 rounded-md">
        {project.status}
      </div>

      <div
        class={`${projectStatus(
          project.status,
        )} rounded-bl-lg bg-blue-600 py-1 text-center -mt-7 pb-8`}>
      </div>
    </div>

  </a>
</li>

```

In the frontmatter part, we add a little function that we use to apply specific classes to the markup depending on the project status, to style it nicely:

```

export function projectStatus(status: string) {
  switch (status) {
    case 'started':
      return ' w-2/12 '
    case 'in progress':
      return ' w-6/12 '
    case 'ongoing':
      return ' w-full bg-blue-600 rounded-br-lg'
    case 'archived':
      return ' w-full bg-zinc-400 rounded-br-lg'
    case 'on hold':
      return ' w-full bg-stripes-darkgray-yellow rounded-br-lg'
    case 'almost finished':
      return ' w-10/12 '
    case 'done':
      return ' w-full bg-green-500 rounded-br-lg'
    case 'not started':
      return ' w-full bg-zinc-400 rounded-br-lg'
  }
}

```

Finally, we add a &lt;style> tag to include 2 custom CSS classes: bg-stripes-darkgray-yellow and dashed-border-top:

```

<style>
  .bg-stripes-darkgray-yellow {
    background-image: repeating-linear-gradient(
      45deg,
      #1f2937,
      #1f2937 25px,
      #f6e711 25px,
      #f6e711 50px
    );
  }

  .dashed-border-top {
    position: relative;
    background-image: repeating-linear-gradient(
      to right,
      currentColor,
      currentColor 7px,
      transparent 7px,
      transparent 20px
    );
    background-size: 100% 2px;
    background-position: top;
    background-repeat: no-repeat;
    border-top: 1px solid transparent;
  }
</style>

```

Here’s the complete **src/components/app/projects/ProjectCard.astro file**:

```

---
const { project } = Astro.props


export function projectStatus(status: string) {
  switch (status) {
    case 'started':
      return ' w-2/12 '
    case 'in progress':
      return ' w-6/12 '
    case 'ongoing':
      return ' w-full bg-blue-600 rounded-br-lg '
    case 'archived':
      return ' w-full bg-zinc-400 rounded-br-lg '
    case 'on hold':
      return ' w-full bg-stripes-darkgray-yellow rounded-br-lg '
    case 'almost finished':
      return ' w-10/12 '
    case 'done':
      return ' w-full bg-green-500 rounded-br-lg '
    case 'not started':
      return ' w-full bg-zinc-400 rounded-br-lg '
  }
}
---

<style>
  .bg-stripes-darkgray-yellow {
    background-image: repeating-linear-gradient(
      45deg,
      #1f2937,
      #1f2937 25px,
      #f6e711 25px,
      #f6e711 50px
    );
  }

  .dashed-border-top {
    position: relative;
    background-image: repeating-linear-gradient(
      to right,
      currentColor,
      currentColor 7px,
      transparent 7px,
      transparent 20px
    );
    background-size: 100% 2px;
    background-position: top;
    background-repeat: no-repeat;
    border-top: 1px solid transparent;
  }
</style>

<li
  class='text-zinc-800 dark:text-white border dark:border-none rounded-lg bg-zinc-100 dark:bg-zinc-800 hover:bg-zinc-200 hover:dark:bg-zinc-700'>
  <a href={`/app/project/${project.id}`}>
    <div
      class='flex justify-center w-full p-6'>
      <h3
        class='text-lg font-bold truncate'>
        {project.name}
      </h3>
    </div>

    <div
      class={`bg-zinc-100 dark:bg-zinc-800 rounded-b-lg text-center border-t ${
        project.status !== 'not started' &&
        project.status !== 'ongoing' &&
        project.status !== 'on hold' &&
        project.status !== 'done' &&
        'border-t-blue-600 dashed-border-top'
      }`}>
      <div
        class="inline-block px-1 mt-[0.35rem] text-sm text-zinc-900 bg-zinc-100 rounded-md">
        {project.status}
      </div>

      <div
        class={`${projectStatus(
          project.status,
        )} rounded-bl-lg bg-blue-600 py-1 text-center -mt-7 pb-8`}>
      </div>
    </div>
  </a>
</li>

```

Looks pretty cool (I changed the status of the projects in PocketBase, to see how it changed its design):

<!-- <img src="../_image3MX.png" alt="image3MX" width=70% /> -->

<img src="/image/_image3MX.png" alt="image3MX" width=70% />

## The problem we are facing with static rendering

[&rarr; top](#)

There is a big problem now that we haven’t yet realized we have.

Astro by default is a static site generator (also called SSG). The site is created at build time, and after that happened, that’s it.

What does this mean, and how does it affect us?

We are currently running Astro in development mode, as we ran npm run dev.

Each time we change something in our pages, the result you see in the browser changes. And new data coming from PocketBase is fetched without issues, as you can see by adding a new project in PocketBase:

<!-- <img src="../_image3PA.webp" alt="image3PA" width=70% /> -->

<img src="/image/_image3PA.webp" alt="image3PA" width=70% />

Now let’s do something.

Let’s build the app for production.

Stop **npm run dev** by pressing **cmd-c** or **ctrl-c** and run:

```

npm run build

```

<!-- <img src="../_image3PB.webp" alt="image3PB" width=70% /> -->

<img src="/image/_image3PB.webp" alt="image3PB" width=70% />

The **build** command is defined in **package.json** as:

<!-- <img src="../_image3PC.webp" alt="image3PC" width=70% /> -->

<img src="/image/_image3PC.webp" alt="image3PC" width=70% />

When you run this command, first Astro runs astro check to check for possible errors, and then, if there are no problems, it runs astro build to create the production version in the dist folder in your project.

You should be able to see dist folder in VS Code:

<!-- <img src="../_image3PD.webp" alt="image3PD" width=70% /> -->

<img src="/image/_image3PD.webp" alt="image3PD" width=70% />

Now run **npm run preview** to run **astro preview**, the Astro command that starts a local server and serves the content of the **dist** folder.

<!-- <img src="../_image3PE.webp" alt="image3PE" width=70% /> -->

<img src="/image/_image3PE.webp" alt="image3PE" width=70% />

Now try accessing the URL, go to the **/app/dashboard** route and you’ll see the projects, as we had before:

<!-- <img src="../_image3PF.webp" alt="image3PF" width=70% /> -->

<img src="/image/_image3PF.webp" alt="image3PF" width=70% />

But now try removing the “new project” you just added - you still see the project on the website!

The reason is that the site was statically built, it was turned to HTML during the build, data was fetched from PocketBase during the build.

You need a new build to get the updated data.

This is great for many different use cases, for example when you have a set of data that’s static and you don’t need to fetch data from the database on any request.

It’s much, much more efficient to build a static site, and deploy on an hosting platform like Netlify or Vercel completely for free.

When you start needing a database, you’ll see things will start costing you a bit of money (or, they’ll have a limited free plan), because that’s a more complex setup.

But this doesn’t work for us, because we are building a dynamic application.

The solution is: we need to enable server-side rendering (SSR) mode in Astro.

## Enable SSR mode in Astro

**(Server Side Rendering)**

[&rarr; top](#)

To enable SSR mode, run the command

```

npm install @astrojs/node@8.2.3

```

If **npm run preview** is still running, terminate the process by using ctrl-c.

Open your **astro.config.mjs** file and add the following:

```

import tailwind from '@astrojs/tailwind'
import { defineConfig } from 'astro/config'

import node from '@astrojs/node'
import 'dotenv/config'

// https://astro.build/config
export default defineConfig({
  integrations: [tailwind()],
  output: 'server',
  adapter: node({
    mode: 'standalone'
  })
})

```

The “adapter” part is interesting because Astro has a lot of server-rendering adapters so it can work anywhere you want to run it on (see https://astro.build/integrations/?search=&categories%5B%5D=adapters)

Node.js is the one we use to run locally, but for example if you want to deploy a site to Cloudflare, you’ll need the Cloudflare adapter. Same for Vercel, Netlify, etc, as all those platforms are special in their own way, so we need a specific adapter to make the best use of them.

output: "server" is what enables SSR for the whole site.

Even though SSR is enabled, we can tell Astro to pre-render at build time some pages, for which we don’t need SSR. Our whole marketing site doesn’t need SSR.

We’ll need to add this line:

```

export const prerender = true

```

at the top of each route, so Astro knows it can prerender them when the server starts.

It’s worth noting you could do the opposite by setting output: "hybrid" in the Astro config, in this case you would set prerender = false for pages you want server-rendered. But since we have just a few pages we want to prerender at build time, and the rest of the site is server rendered on each request, we’ll stick to server.

Actually let’s go and make the homepage prerendered in src/pages/index.astro:

```

---
export const prerender = true

import LayoutSite from '@layouts/LayoutSite.astro'

//...

```

Do the same for **src/pages/blog.astro** and also **src/pages/blog/[slug].astro**.

Now run **npm run build** again, notice some things changed compared to the last time we ran that command:

<!-- <img src="../_image3PG.webp" alt="image3PG" width=70% /> -->

<img src="/image/_image3PG.webp" alt="image3PG" width=70% />

Now run **npm run preview**, this command changed too:

<!-- <img src="../_image3PH.webp" alt="image3PH" width=70% /> -->

<img src="/image/_image3PH.webp" alt="image3PH" width=70% />

Now go to **http://localhost:4321/app/dashboard**, and now try doing what we tried before - adding a new project in PocketBase, or deleting a new one.

After reloading the page, you’ll see the new data reflected on the website.

## SSR vs SSG mode

**Server Side Rendering vs Server Side Generator**

[&rarr; top](#)

The upside is that we now have fresh data.

The downside is that we have to look in the database for every request (we’ll be able to speed up things when we’ll talk about caching).

The time needed for this will be super fast locally.

It will aslo be very fast on a remote server if both Astro and PocketBase are on the same machine or data center.

Speed problems will start when you put the website somewhere on the cloud, for example in a US East data center, but data is hosted in a data center in US West or Europe - always try to keep data and server very near each other, geographically.

A static site can be made super fast by serving it from multiple locations, that’s what most hosting providers do automatically with their CDN and Edge offering.

A SSR site with a database is trickier, but there are ways to do so - might be out of the scope of the Bootcamp.

We’ll focus on deploying, in the last module, but in a centralized location - you’ll pick the one that’s nearest to the majority of your app users.

This site you’re reading is server-rendered from a super cheap plan on Render, from Oregon, and is very fast for me even though I’m very far from it.

Now that we have SSR enabled, stop npm run preview and let’s go back to running npm run dev to go back to development mode, so changes to your code will be immediately reflected on the site.

The production build is more optimized. And development mode ships a “client” script to enable “hot module reloading” (that’s the magic that happens when the app refreshes when you save a file in your editor).

## Add a way to create a new project from the app

[&rarr; top](#)

Now that we’re back in development mode, let’s add a way to create a new project from the app.

We start build our “app experience”.

First, I want to add a new button at the end of our projects list with the “Add new” words in it.

Create a new component **AddNewProjectCard** in **src/components/app/projects/AddNewProjectCard.astro**

Edit the file by adding the following code:

```

<div class='text-white bg-zinc-800 rounded-lg shadow'>
  <div
    class='flex items-center justify-between w-full p-6 text-center space-x-6'>
    <div class='flex-1 mx-auto'>
      <button
        type='button'
        class='inline-flex items-center justify-center px-6 py-2 text-sm font-bold text-white bg-blue-600 border border-transparent rounded-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500 select-none'>
        Add new project
      </button>
    </div>
  </div>
</div>

```

At the moment this button does nothing, it just renders the button on the page.

We add this component in **src/pages/app/dashboard.astro**

```

---
import PocketBase from 'pocketbase'

import LayoutApp from '@layouts/LayoutApp.astro'

import ProjectCard from '@components/app/projects/ProjectCard.astro'
import AddNewProjectCard from '@components/app/projects/AddNewProjectCard.astro'

const pb = new PocketBase('http://127.0.0.1:8090')

const projects = await pb
  .collection('projects')
  .getFullList()
---

<LayoutApp title='Dashboard'>
  <div
    class='py-10 mx-auto text-white max-w-7xl space-y-6'>
    <div
      class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 text-xl sm:text-3xl md:text-5xl text-white uppercase text-center font-extrabold'>
      Projects
    </div>

    <div class='space-y-6'>
      <ul class='grid gap-6 sm:grid-cols-2'>
        {
          projects.map(project => (
            <ProjectCard project={project} />
          ))
        }
      </ul>
      <AddNewProjectCard />
    </div>
  </div>
</LayoutApp>

```

You should see the button in place:

<!-- <img src="../_image3PJ.webp" alt="image3PJ" width=70% /> -->

<img src="/image/_image3PJ.webp" alt="image3PJ" width=70% />

Now comes the interesting part part.

What should happen when you click the “Add new” button? Perhaps we send the user to a new page, maybe a /app/projects/new route, where there is a form, the user adds the project name, saves, we send them back to /app/dashboard.

That’s a perfectly reasonable thing to do.

However, the page would look quite empty because the form is a really small one.

It’s better, I think, to show this form inside a modal. User clicks “Add new”, a little window shows up, the user hits save, and we display the new project right there.

We’re going to have a lot of those little interactions:

- to add a new project (this use case)
- to add a new task
- to add a new team

but also to edit a project’s name, or a team’s name.

So we’ll build a “modal container” in a very generic way that can be reused for everything.

## Create a modal container

[&rarr; top](#)

We’ll use the &lt;dialog> HTML element for the modal.

This is a recent browser feature, and it’s perfect to create modal windows.

Read more about this on https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dialog.

By default the content of a &lt;dialog> element is hidden, and we show it to the user by first looking up the dialog:

```

document.querySelector('dialog')

```

and then calling its **showModal()** method:

```

document.querySelector('dialog').showModal()

```

We can close the dialog by pressing the “esc” key, this automatically closes the dialog for us without having to write any code.

Or, we can programmatically close it by using JavaScript:

```

document.querySelector('dialog').close()

```

Let's start by adding a **&lt;dialog>** element in **src/layouts/LayoutApp.astro**:

```

---
const { title = 'Spring24app' } = Astro.props
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
    <title>{title}</title>
    <meta
      name='description'
      content='A project management tool'
    />
  </head>

  <body>
    <main
      class='min-h-screen dark:bg-black dark:text-white'>
      <div class='max-w-5xl px-4 py-4 mx-auto'>
        <dialog></dialog>
        <slot />
      </div>
    </main>
  </body>
</html>

```

This will be the container of our project modal.

We'll write the modal content in a new page component.

Let's create a new folder where we'll store all the modal page components: **src/page/app/modals/**. Inside it, create **project/new.astro**.

We'll be able to get this page using the URL **/modals/project/new**.

This will be an **HTML partial**. It won't be a full HTML page, it will be just something we'll put inside the &lt;dialog> HTML element, so it can be just some HTML tag.

Add the following HTML into it to center a visual container with a gray background, and add some text into it:

```

---
export const partial = true
---

<div class='fixed inset-0'>
  <div class='flex items-center justify-center h-screen'>
    <div class='bg-zinc-100 dark:bg-zinc-800 rounded-lg max-w-sm w-full p-6 space-y-6'>
      <p>modal</p>
    </div>
  </div>
</div>

```

This is a page partial (see https://astro.build/blog/astro-340/ and https://docs.astro.build/en/basics/astro-pages/#partials)

We’ll later implement this, but let’s get to the point this content is shown in the page.

To do this, we’ll load the HTML partial inside the &lt;dialog> HTML element when the “Add new” button is clicked.

How? Using **htmx**.

## What is htmx??

[&rarr; top](#)

htmx is a wonderful tiny library that allows us to perform actions and make our app feel like it’s built with a complex JavaScript framework, while in reality it’s not.

If you’ve used React or Vue or Svelte or any of those frameworks before, you’ll find htmx really simple to use, yet powerful.

It’s peculiar for a JavaScript library, because it uses HTML as a transport layer, instead of JSON as we’re used to do with heavy frontend frameworks like React, Angular, Vue, Svelte.

By now you should have installed it (version )First let’s install it.

You can install htmx simply by adding a &lt;script> tag to the &lt;head> of the app layout, but since we use TypeScript in our project, we can benefit from using htmx’s types definitions which you get “for free” by adding htmx from npm.

Install it from the terminal:

```

npm install htmx.org@1.9.10

```

Then import it in the layout src/layouts/LayoutApp.astro:

```

---
const { title = 'Spring24app' } = Astro.props
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
    <title>{title}</title>
    <meta
      name='description'
      content='A project management tool'
    />

    <script>
      import * as htmx from 'htmx.org'

      declare global {
        interface Window {
          htmx: any
        }
      }

      window.htmx = htmx //optional

      htmx.process(document.body)
    </script>
  </head>

  <body>
    <main
      class='min-h-screen dark:bg-black dark:text-white'>
      <div class='max-w-5xl px-4 py-4 mx-auto'>
        <dialog></dialog>
        <slot />
      </div>
    </main>
  </body>
</html>

```

Doing so now you have all the documentation and hints about htmx right in VS Code:

We add the line **window.htmx = htmx** in case we want to access the htmx object in other pages, so we don’t have to pass it around.

## Show the modal

[&rarr; top](#)

Now that htmx is loaded, add these 2 lines to the **src/components/app/projects/AddNewProjectCard.astro** component:

```

<div class='text-white bg-zinc-800 rounded-lg shadow'>
  <div
    class='flex items-center justify-between w-full p-6 text-center space-x-6'>
    <div class='flex-1 mx-auto'>
      <button
        type='button'
        class='inline-flex items-center justify-center px-6 py-2 text-sm font-bold text-white bg-blue-600 border border-transparent rounded-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500 select-none'
        hx-get='/app/modals/project/new'
        hx-target='dialog'
      >
        Add new project
      </button>
    </div>
  </div>
</div>

```

This tells htmx to get the HTML returned by the URL **/modals/project/new** (the page route we just created above), and put it inside the &lt;dialog> element.

We just have one dialog element in our app, and I don’t think we’ll need more, so we’ll just target it this way.

Otherwise you could have used any CSS selector, like **#modal** for example.

Now try clicking “Add new”.

Nothing seems to happen, but if you look at the network panel in the devtools you’ll see a request to
**/modals/project/new**:

fig3RA

If you open the details of this request you’ll see the HTML we wrote in the page partial we wrote:

And notice how fast the request is, just 7ms.

This HTML we retrieved was added to the &lt;dialog> tag by htmx:

This is the first time we used htmx, but notice how much stuff it did behind the scenes, just by adding those 2 lines:

```

hx-get='/app/modals/project/new'
hx-target='dialog'

```

Why don’t we see the content on the page, though?

It’s because the &lt;dialog> element is a bit special, as I mentioned before, its content is hidden by default.

We need to use a line of JavaScript to **src/pages/app/modals/project/new.astro** to tell it to show the content:

```

---
export const partial = true
---

<script is:inline>
  document.querySelector('dialog').showModal()
</script>

<div class='fixed inset-0'>
  <div class='flex items-center justify-center h-screen'>
    <div
      class='bg-zinc-100 dark:bg-zinc-800 rounded-lg max-w-sm w-full p-6 space-y-6'>
      <p>modal</p>
    </div>
  </div>
</div>

```

We can now add a special &lt;dialog>-specific CSS line in **src/layouts/LayoutApp.astro** to make all the content “behind” the dialog to blur:

```

---
const { title = 'Spring24app' } = Astro.props
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
    <title>{title}</title>
    <meta
      name='description'
      content='A project management tool'
    />

    <script>
      import * as htmx from 'htmx.org'

      declare global {
        interface Window {
          htmx: any
        }
      }

      window.htmx = htmx //optional

      htmx.process(document.body)
    </script>

    <style>
      dialog::backdrop {
        background-color: rgba(0, 0, 0, 0.7);
        backdrop-filter: blur(3px);
      }
    </style>
  </head>

  <body>
    <main
      class='min-h-screen dark:bg-black dark:text-white'>
      <div class='max-w-5xl px-4 py-4 mx-auto'>
        <dialog></dialog>
        <slot />
      </div>
    </main>
  </body>
</html>

```

## Add the form to the modal

[&rarr; top](#)

Now that our modal appears on the screen, let’s add the form into it.

We’ll do a bit of groundwork too, to make it possible to easily reuse what we’ll do for other modals, too.

We create a **src/components/app/modals/** folder to host the modal - specific components.

In there, we create **ModalLayout.astro**.

We’re going to reuse this across all the modals.

This component gets a title through its props, and has a **&lt;slot />** element inside it, so basically we can add more HTML and components by requiring it, and passing content as its child elements.

```

---
const { title } = Astro.props
---

<script is:inline>
  document.querySelector('dialog').showModal()
</script>

<div class='fixed inset-0'>
  <div class='flex items-center justify-center h-screen'>
    <div
      class='bg-zinc-100 dark:bg-zinc-800 rounded-lg max-w-sm w-full p-6 space-y-6'>
      <h3
        class='text-lg font-bold text-zinc-800 dark:text-white leading-6 text-center'>
        {title}
      </h3>
      <div>
        <slot />
      </div>
    </div>
  </div>
</div>

```

We’re going to use this layout in **src/pages/app/modals/project/new**.astro, replacing the pre-existing content:

```


---
export const partial = true

import ModalLayout from '@components/app/modals/ModalLayout.astro'
---

<ModalLayout title='New project'>
  <p class='text-white'>Hello</p>
</ModalLayout>

```

See how we pass the **title** prop, and that is reflected in the modal. Also, we pass child HTML elements inside the **ModalLayout** element, and they are put inside the modal thanks to our use of &lt;slot />.

Let’s now add the actual modal we’ll use to add a new project. We’re going to have an input field for the name, and 2 buttons, one to add the project, another one to cancel.

I’ll extract those 3 components to their own files, as we’ll reuse them later:

**src/components/app/modals/ButtonCancel.astro**

```

<button
  aria-label='Close dialog'
  type='button'
  class='inline-flex justify-center px-4 py-2 ml-3 font-medium text-gray-700 bg-white border border-gray-300 rounded-md shadow-sm hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500 mt-0 w-auto text-sm'
  onclick="document.querySelector('dialog')?.close()">
  Cancel
</button>

```

(notice how we close the modal when the button is clicked)

**src/components/app/modals/ButtonSubmit.astro**

```


---
const { label = 'Add' } = Astro.props
---

<button
  type='submit'
  class='inline-flex justify-center px-4 py-2 font-medium text-white bg-blue-600 border border-transparent rounded-md shadow-sm hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500 w-auto text-sm'>
  {label}
</button>

```

(notice how we can customize the label by adding a **label** prop)

**src/components/app/modals/InputField.astro**

```

---
const { name, value } = Astro.props
---

<input
  id={name}
  name={name}
  value={value}
  type='text'
  required
  class='block w-full px-3 py-2 placeholder-gray-400 border border-gray-300 appearance-none rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500 sm:text-sm'
/>

```

(notice we can reuse this for different **name** and **value** by passing props)

Let’s put those 3 components into use in src/pages/app/modals/project/new.astro:

```

---
export const partial = true

import ModalLayout from '@components/app/modals/ModalLayout.astro'
import ButtonSubmit from '@components/app/modals/ButtonSubmit.astro'
import ButtonCancel from '@components/app/modals/ButtonCancel.astro'
import InputField from '@components/app/modals/InputField.astro'
---

<ModalLayout title='New project'>
  <form class='space-y-6' hx-post='/app/api/projects'>
    <div>
      <div class='mt-1'>
        <InputField name='project_name' />
      </div>
    </div>
    <div class='flex justify-center'>
      <ButtonSubmit />
      <ButtonCancel />
    </div>
  </form>
</ModalLayout>

```

Note how the input field is automatically set to focus by the browser, thanks to the use of the &lt;dialog> element.

## Close the modal when we click outside of it

[&rarr; top](#)

Also note how the modal is closed when we press the “esc” button. This is a browser feature, also thanks to the use of the &lt;dialog> element.

It would be cool if we could close the modal also when the user clicks outside of it.

To do this, we’d need to write quite a bit of JavaScript.

This could be the logic to implement:

```

function onClickOutside(element, callback) {
  document.addEventListener('click', (event) => {
    if (!element.contains(event.target)) {
      callback()
    }
  }, true)
}

const targetElement = document.querySelector('#yourElementId')

onClickOutside(targetElement, () => {
  document.querySelector('dialog').close()
})

```

Read chapter on events on W3S or MDN

Instead, however, we’re going to introduce a library we’ll use for several of those little things and interactions: Alpine.js.

With Alpine.js, all this JavaScript can be turned into 1 line:

```

@click.outside.capture="document.querySelector('dialog').close()"

```

See this page on the Alpine.js documentation https://alpinejs.dev/directives/on for reference.

We’d use this as an HTML attribute on the element we want to detect the “click outside”.

First however we need to install Alpine.js (if not installed yet)

We do so using npm:

```

npm install alpinejs@3.13.7

npm install --dev @types/alpinejs@3.13.9

```

Then in our **src/layouts/LayoutApp.astro** we include it:

```

---
const { title = 'Spring24app' } = Astro.props
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
    <title>{title}</title>
    <meta
      name='description'
      content='A project management tool'
    />

    <script>
      import * as htmx from 'htmx.org'
      import Alpine from 'alpinejs'

      declare global {
        interface Window {
          htmx: any
          Alpine: any
        }
      }

      window.htmx = htmx //optional
      window.Alpine = Alpine //optional

      Alpine.start()

      htmx.process(document.body)
    </script>

    <style>
      dialog::backdrop {
        background-color: rgba(0, 0, 0, 0.7);
        backdrop-filter: blur(3px);
      }
    </style>
  </head>

  -<body>  //DELETE
  +<body x-data>
    <main
      class='min-h-screen dark:bg-black dark:text-white'>
      <div class='max-w-5xl px-4 py-4 mx-auto'>
        <dialog></dialog>
        <slot />
      </div>
    </main>
  </body>
</html>

```

Now in **src/components/app/modals/ModalLayout.astro** we add:

```

---
const { title } = Astro.props
---

<script is:inline>
  document.querySelector('dialog').showModal()
</script>

<div class='fixed inset-0'>
  <div class='flex items-center justify-center h-screen'>
    <div
      class='bg-zinc-100 dark:bg-zinc-800 rounded-lg max-w-sm w-full p-6 space-y-6'
      @click.outside.capture="document.querySelector('dialog').close()">
      <h3
        class='text-lg font-bold text-zinc-800 dark:text-white leading-6 text-center'>
        {title}
      </h3>
      <div>
        <slot />
      </div>
    </div>
  </div>
</div>

```

…and the modal closes when we click outside of it.

## Create the new project

[&rarr; top](#)

When the “Add” button is pressed, right now nothing happens.

Actually, something happens: htmx makes a **POST** request to **/app/api/projects**, which results in a **404 Not Found** response as we haven’t created this route yet.

<!-- <img src="../_image46.png" alt="" width=70%> -->
<img src="/image/_image46.png" alt="" width=70%>

As you can see if you switch to the request Payload tab, you’ll see the project_name input field value was correctly sent to the server, as we expect a form to do:

<!-- <img src="../_image47.png" alt="" width=70%> -->
<img src="/image/_image47.png" alt="" width=70%>

Check out the network tab in chrome developer tools. The **project_name** input field value was correctly sent to the server.

If you remember, in the **src/pages/app/dashboard.astro** file we used those lines to retrieve the projects list:

```

import PocketBase from 'pocketbase'

const pb = new PocketBase('http://127.0.0.1:8090')

const projects = await pb
  .collection('projects')
  .getFullList()

```

Since we’re going to work a lot with PocketBase and its data APIs, let’s move this to a separate file.

Create a **src/data** folder, and inside it create the **pocketbase.ts** file.

Let’s add:

```

import PocketBase from 'pocketbase'

export const pb = new PocketBase('http://127.0.0.1:8090')

```

actually let’s store the PocketBase URL in the **.env** file, that’s were we store the environment variables.

Create it first, in the project root (along with **astro.config.mjs** and **package.json**), then add:

```

POCKETBASE_URL=http://127.0.0.1:8090

```

<!-- <img src="../_image(48).png" alt="" width=70%> -->
<img src="/image/_image(48).png" alt="" width=70%>

After creating the file, restart the npm run dev process.

Now change the line to initialize PocketBase to this:

```

export const pb = new PocketBase(import.meta.env.POCKETBASE*URL ||
process.env.POCKETBASE_URL)

```

NOTE: on localhost in dev mode (npm run dev), we get env vars using import.meta.env.\*, but when deploying on a server we get vars using process.env.\_. This is why I use the syntax import.meta.env.POCKETBASE_URL || process.env.POCKETBASE_URL to get the first one, if defined, or the second one if the first is not defined.

If you see an error like “Something went wrong while processing your request.”, see the troubleshooting section at the end of this page.

If you see this error:

<!-- <img src="../_image(50).png" alt="" width=70%> -->
<img src="/image/_image(50).png" alt="" width=70%>

to fix it, run:

```

npm install --save-dev @types/node

```

Create a **getProjects** function now that will retrieve the projects list:

```

import PocketBase from 'pocketbase'

export const pb = new PocketBase(import.meta.env.POCKETBASE_URL ||
process.env.POCKETBASE_URL)

export async function getProjects() {
const projects = await pb
.collection('projects')
.getFullList()

return projects
}

```

Use this in **src/pages/app/dashboard.astro**:

```

import PocketBase from 'pocketbase'  //DELETE

const pb = new PocketBase('http://127.0.0.1:8090')

const projects = await pb
.collection('projects')
.getFullList()

import { getProjects } from '@data/pocketbase'

const projects = await getProjects()

```

Things should work as before in the dashboard.

Let’s now implement an **addProject()** function in **src/data/pocketbase.ts**:

```

export async function addProject(name: string) {
const newProject = await pb.collection('projects')
.create({
name,
status: 'not started',
})

return newProject
}

```

Now create **src/pages/app/api/**.

We create this “API” folder as this will be the place for our “HTML API”. We’ll handle

```

POST, GET, PUT requests

```

to the resources we manage, and we’ll respond with HTML partials.

In there create the **projects.astro** file as we’re going to respond to a POST request to **/app/api/projects**, we fetch the project_name from the request **formData** object, and we then call **addProject()** to add the project to PocketBase:

```

---

export const partial = true

import { addProject } from '@data/pocketbase'

if (Astro.request.method === 'POST') {
const formData = await Astro.request.formData()

const project_name = formData.get('project_name')?.toString() || ''

const project = await addProject(project_name)
}

---

```

The call to **/app/api/projects** should now work and return a 200 OK response.

Try it!

The new project was added to PocketBase, and you’ll see it if you refresh the page, however right now we see this:

<!-- <img src="../_image(51).png" alt="" width=70%> -->
<img src="/image/_image(51).png" alt="" width=70%>

Why?

By default htmx replaces the innerHTML (the content) of the element that triggers the HTTP request.

And we returned no HTML at all from our request, so htmx just replaced the existing HTML with nothing.

The easiest thing we can do now is to add a special htmx header to the response called **HX-Redirect** in **src/pages/app/api/projects.astro**, like this:

```

---

export const partial = true

import { addProject } from '@data/pocketbase'

if (Astro.request.method === 'POST') {
const formData = await Astro.request.formData()

const project_name = formData
.get('project_name')
as string

const project = await addProject(project_name)

Astro.response.headers.set('HX-Redirect', `/app/dashboard`)
}

---

```

TIP: “as string” is a way to tell TypeScript this is a string even when the value could be undefined

After just adding this line, htmx when gets the response back (an empty document, actually, since we didn’t return any HTML from our “HTML API” partial page), will redirect the user to the **/app/dashboard** page.

It’s all happening so fast we didn’t even notice we have an additional request on top.

This is just one of the things you can do with htmx, you can fine-tune this later to send specific HTML to update the projects list, for example, but I think it’s fine to start with.

## Create the single project page

[&rarr; top](#)

Let’s now create the single project page.

Create the **src/pages/app/project** folder, and inside it, add **[project_id].astro**.

This will handle the /app/project/<project_id> URLs.

Just type “Project page” in this file, you should see this if you click a link to a project from the dashboard:

<!-- <img src="../_image(52).png" alt="" width=70%> -->
<img src="/image/_image(52).png" alt="" width=70%>

Let’s make this pretty, and let’s fetch the project name from PocketBase.

Add this to **src/data/pocketbase.ts**:

```

export async function getProject(id: string) {
const project = await pb.collection('projects').getOne(id)

return project
}

```

We’ll use this in **src/pages/app/project/[project_id].astro**.

First we retrieve the **project_id** value from **Astro.params**.

If we don’t get a project corresponding to the **id** from the **getProject()** call, we redirect back to the dashboard (notice this doesn’t work now because **getProject()** raises an exception, so we’d need to wrap this into a try/catch, but we’ll do this later.

Otherwise we show the project name in the UI:

```
---

import LayoutApp from '@layouts/LayoutApp.astro'
import { getProject } from '@data/pocketbase'

const { project_id = '' } = Astro.params

const project = await getProject(project_id)

if (!project) {
return Astro.redirect('/app/dashboard')
}

---

<LayoutApp title={project.name}>
  <div
    class='py-10 mx-auto text-white max-w-7xl space-y-6'>
    <div
      class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 text-xl sm:text-3xl md:text-5xl text-white uppercase text-center font-extrabold'>
      {project.name}
    </div>
  </div>
</LayoutApp>

```

We’ve got it:

<!-- <img src="../_image(53).png" alt="" width=70%> -->
<img src="/image/_image(53).png" alt="" width=70%>

## Add a way to add tasks to a project

[&rarr; top](#)

On the same file, **src/pages/app/project/[project_id].astro**, let’s create a “box” to list tasks on the page:

```
---

import LayoutApp from '@layouts/LayoutApp.astro'
import { getProject } from '@data/pocketbase'

const { project_id = '' } = Astro.params

const project = await getProject(project_id)

if (!project) {
return Astro.redirect('/app/dashboard')
}

---

<LayoutApp title={project.name}>
  <div
    class='py-10 mx-auto text-white max-w-7xl space-y-6'>
    <div
      class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 text-xl sm:text-3xl md:text-5xl text-white uppercase text-center font-extrabold'>
      {project.name}
    </div>

    <div class='space-y-6'>
      <div
        class='p-10 text-white rounded-lg shadow bg-zinc-100 dark:bg-zinc-800'>
        <h2
          class='pb-10 text-xl font-black text-center uppercase text-zinc-800 dark:text-white'>
          Tasks to do
        </h2>
      </div>
    </div>

  </div>
</LayoutApp>

```

Now we create a button to add a new task.

Create the folder **src/components/app/tasks**, we’ll store all tasks-related components here.

Create **ButtonAddNewTask.astro**:

```

---

const { project_id } = Astro.props
---

<div class='w-full mx-auto text-center'>
  <button
    type='button'
    class='inline-flex items-center justify-center px-6 py-2 text-sm font-bold text-white bg-blue-600 border border-transparent rounded-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500 select-none'
    hx-get=`/app/modals/project/${project_id}/task/new`
    hx-target='dialog'>
    Add new
  </button>
</div>

```

Now you can import and add this component to **src/pages/app/project/[project_id].astro**:

```

---

import LayoutApp from '@layouts/LayoutApp.astro'
import { getProject } from '@data/pocketbase'

import ButtonAddNewTask from '@components/app/tasks/ButtonAddNewTask.astro'

const { project_id = '' } = Astro.params

const project = await getProject(project_id)

if (!project) {
return Astro.redirect('/app/dashboard')
}

---

<LayoutApp title={project.name}>
  <div
    class='py-10 mx-auto text-white max-w-7xl space-y-6'>
    <div
      class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 text-xl sm:text-3xl md:text-5xl text-white uppercase text-center font-extrabold'>
      {project.name}
    </div>

    <div class='space-y-6'>
      <div
        class='text-white rounded-lg shadow p-10 bg-zinc-100 dark:bg-zinc-800'>
        <h2
          class='pb-10 text-xl font-black text-center uppercase text-zinc-800 dark:text-white'>
          Tasks to do
        </h2>

        <ButtonAddNewTask project_id={project_id} />
      </div>
    </div>

  </div>
</LayoutApp>

```

You should see the button.

The button loads the HTML partial content coming from the page route **/modals/project/${project_id}/task/new**

Create the file **src/pages/app/modals/project/[project_id]/task/new.astro** (and all the folders needed to create it)

In this file we build a form similarly to what we did in **src/pages/app/modals/project/new.astro**.

What changes (apart from changing from “project” to “task”) is we now get the project_id from the URL, and we use it to build the correct **hx-post** value:

```

---

export const partial = true

import ModalLayout from '@components/app/modals/ModalLayout.astro'
import ButtonSubmit from '@components/app/modals/ButtonSubmit.astro'
import ButtonCancel from '@components/app/modals/ButtonCancel.astro'
import InputField from '@components/app/modals/InputField.astro'

## const { project_id } = Astro.params

<ModalLayout title='New task'>
  <form
    class='space-y-6'
    hx-post={`/app/api/project/${project_id}/task`}>
    <div>
      <div class='mt-1'>
        <InputField name='task_text' />
      </div>
    </div>
    <div class='flex justify-center'>
      <ButtonSubmit />
      <ButtonCancel />
    </div>
  </form>
</ModalLayout>

```

You should now see this show up if you click the “Add task” button:

<!-- <img src="../_image(56).png" alt="" width=70%> -->
<img src="/image/_image(56).png" alt="" width=70%>

This form uses htmx, through the use of the **hx-post** attribute, to POST data to **/app/api/project/${project_id}/task**.

Let’s create this route by adding the file **src/pages/app/api/project/[project_id]/task.astro**

In there we’ll handle the POST request and we’ll send the project id and the task text to an **addTask()** function that we’ll now write in **pocketbase.ts**.

Once the task is added, we use the **HX-Redirect** to simply tell the client to reload the project page, which will automatically fetch the new task.

```
---

export const partial = true

import { addTask, getProject } from '@data/pocketbase'

const { project_id = '' } = Astro.params

const project = await getProject(project_id)

if (Astro.request.method === 'POST') {
const formData = await Astro.request.formData()
const task_text =
formData.get('task_text') as string

await addTask(project_id, task_text)

Astro.response.headers.set(
'HX-Redirect',
`/app/project/${project_id}`
)
}

---

```

Switch to **src/data/pocketbase.ts** and add this:

```

export async function addTask(
project_id: string,
text: string
) {
const newTask = await pb.collection('tasks').create({
project: project_id,
text,
})

return newTask
}

```

Tasks are now saved to PocketBase!

## List the project tasks

[&rarr; top](#)

Now that we have tasks, it’s time to list the tasks in the project page.

Add a **getTasks()** function to pocketbase.ts:

```

export async function getTasks(project_id: string) {
const options = {
filter: `project = "${project_id}"`,
}

const tasks = await pb
.collection('tasks')
.getFullList(options)

return tasks
}

```

We use this in **src/pages/app/project/[project_id].astro**:

```

---

import LayoutApp from '@layouts/LayoutApp.astro'
import { getProject } from '@data/pocketbase'
import { getProject, getTasks } from '@data/pocketbase'

import ButtonAddNewTask from '@components/app/tasks/ButtonAddNewTask.astro'

const { project_id = '' } = Astro.params

const project = await getProject(project_id)

if (!project) {
return Astro.redirect('/app/dashboard')
}

const tasks = await getTasks(project_id)

<LayoutApp title={project.name}>
  <div
    class='py-10 mx-auto text-white max-w-7xl space-y-6'>
    <div
      class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 text-xl sm:text-3xl md:text-5xl text-white uppercase text-center font-extrabold'>
      {project.name}
    </div>

    <div class='space-y-6'>
      <div
        class='text-white rounded-lg shadow p-10 bg-zinc-100 dark:bg-zinc-800'>
        <h2
          class='pb-10 text-xl font-black text-center uppercase text-zinc-800 dark:text-white'>
          Tasks to do
        </h2>

        <div>
          {
            tasks.length === 0 && (
              <p class='text-center text-zinc-900 dark:text-white pb-10'>
                Nothing yet
              </p>
            )
          }

          <ul class='space-y-6'>
            {tasks.map(task => <li>{task.text}</li>)}
          </ul>
        </div>

        <ButtonAddNewTask project_id={project_id} />
      </div>
    </div>

  </div>
</LayoutApp>

```

The **tasks.length === 0 && ()** part is a way, in Astro components (and React’s JSX) to include the part inside parentheses only if the condition is true. In this case we show “Nothing yet” if the tasks number is 0.

Here is the result, after adding some sample tasks:

<!-- <img src="../_image(57).png" alt="" width=70%> -->
<img src="/image/_image(57).png" alt="" width=70%>

## Troubleshooting

[&rarr; top](#)

Here are some common errors you might stumble upon.

If you see an error like “Something went wrong while processing your request.”

<!-- <img src="../_image(58).png" alt="" width=70%> -->
<img src="/image/_image(58).png" alt="" width=70%>

it means Astro cannot connect to PocketBase. Double-check PocketBase is running, and you set the connection URL value (usually POCKETBASE_URL=http://127.0.0.1:8090) in the .env file.

Double-check the .env file is in the root folder of your project, in the same folder where there’s package.json (not inside src, for example).

Restart npm run dev when changing your .env file content.

Then also double-check this variable is picked up correctly in src/data/pocketbase.ts

```

console.log(
import.meta.env.POCKETBASE_URL ||
process.env.POCKETBASE_URL
)

```

and check what this prints to the console (restart npm run dev again)

Another issue I’ve seen is permissions on PocketBase collections.

If you get an error page saying “Only admins can perform this action”, make sure permissions are open to everyone, as you can see in those screenshots, for both projects and tasks:

<!-- <img src="../_image(59).png" alt="" width=70%> -->
<img src="/image/_image(59).png" alt="" width=70%>

<!-- <img src="../_image(60).png" alt="" width=70%> -->
<img src="/image/_image(60).png" alt="" width=70%>

and that those settings are saved.

If you see a “Failed to create record” error when creating a project, check that the ‘status’ field in the projects PocketBase collection has all these options: not started, started, in progress, almost finished, done, ongoing, on hold, archived

<!-- <img src="../_image(61).png" alt="" width=70%> -->
<img src="/image/_image(61).png" alt="" width=70%>

Any time there is a PocketBase-related error that’s a bit vague, try looking in the PocketBase logs page at **http://localhost:8090/\_/?#/logs**

For example here I erroneously renamed the project field of the tasks collection to projects, so the filter for project didn’t work and I got this error “invalid left operand “project” - unknown field “project"" - this can point you in the right direction.

<!-- <img src="../_image(62).png" alt="" width=70%> -->
<img src="/image/_image(62).png" alt="" width=70%>

To make things easier, if you type “error” in the search bar and press enter, PocketBase will show all the requests that resulted in an error.

## Wrapping up

[&rarr; top](#)

In this module we started to see how we can interface Astro and PocketBase to fetch and store data.

We’ve also started using **htmx** and **Alpine** to help us create interactive experiences on our pages.

It’s a lot of new stuff! But you’ve been introduced to the entire stack we’ll be using, for the next modules we’ll be adding features and crafting the application user experience by using this core set of technologies: Astro, PocketBase, htmx, Alpine.js, gradually learning how to use those tools to do everything we need.

## content of this module

1. [Introduction to the module](#introduction)
2. [Create a dashboard](#create-a-dashboard)
3. [Start fetching data from PocketBase](#start-fetching-data-from-pocketbase)
4. [Show the projects list on the page](#show-the-projects-list-on-the-page)
5. [Create a layout for the app](#create-a-layout-for-the-app)
6. [Show projects nicely](#show-projects-nicely)
7. [Show the project status](#show-the-project-status)
8. [The problem we’re facing with static site rendering](#the-problem-we-are-facing-with-static-rendering)
9. [Enable SSR mode in Astro](#enable-ssr-server-side-rendering-mode-in-astro)
10. [SSR vs SSG mode](#ssr-vs-ssg-mode)
11. [Add a way to create a new project from the app](#add-a-way-to-create-a-new-project-from-the-app)
12. [Create a modal container](#create-a-modal-container)
13. [Time to introduce htmx](#what-is-htmx)
14. [Show the modal](#show-the-modal)
15. [Add the form to the modal](#add-the-form-to-the-modal)
16. [Close the modal when we click outside of it](#close-the-modal-when-we-click-outside-of-it)
17. [Create the new project](#create-the-new-project)
18. [Create the single project page](#create-the-single-project-page)
19. [Add a way to add tasks to a project](#add-a-way-to-add-tasks-to-a-project)
20. [List the project tasks](#list-the-project-tasks)
21. [Troubleshooting](#troubleshooting)
22. [Wrapping up](#wrapping-up)

[&rarr; top](#)
