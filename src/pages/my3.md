# Module 3 week 5.18

We build a pretty cool site with a homepage built using a component-based approach.

We used content collections to create a blog.

The site works on mobile or desktop, looks nice in light or dark mode.

The website is statically pre-rendered at build time.

What does this mean? Basically, when you deploy the site, Astro generates the HTML, and that’s it.

In the this and following modules we’ll add Server-Side Rendering (SSR) in order to make our application dynamic, but what you’ve built so far is a static site that can be deployed on a simple hosting platform like Netlify or Cloudflare Pages without any more work to do.

## Content

1.	Introduction to the module
2.	Create a dashboard
3.	Start fetching data from PocketBase
4.	Show the projects list on the page
5.	Create a layout for the app
6.	Show projects nicely
7.	Show the project status
8.	The problem we’re facing with static site rendering
9.	Enable SSR mode in Astro
10.	SSR vs SSG mode
11.	Add a way to create a new project from the app
12.	Create a modal container
13.	Time to introduce htmx
14.	Show the modal
15.	Add the form to the modal
16.	Close the modal when we click outside of it
17.	Create the new project
18.	Create the single project page
19.	Add a way to add tasks to a project
20.	List the project tasks
21.	Troubleshooting
22.	Wrapping up

## Introduction

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

Create the folder **src/pages/app** and inside it create the file **dashboard.astro**

Now visit the URL **http://localhost:4321/app/dashboard**.

You'll see a blank page.

<img src="../_image3MA.webp" alt="image3MA" width=100% />
<img src="/_image3MA.webp" alt="image3MA" width=100% />

In Astro, if there’s no page route corresponding to a URL, you’ll see a “404 not found” page:

<img src="../_image3MB.webp" alt="image3MA" width=100% />
<img src="  /_image3MB.webp" alt="image3MA" width=100% />

404 is the HTTP response status code for “page not found”. The HTTP server returns this status code to the client.

You can see the HTTP response status code in the **DevTools Network panel**:

<img src="../_image3MC.webp" alt="image3MA" width=100% />
<img src="  /_image3MC.webp" alt="image3MA" width=100% />

<img src="../_image3MD.webp" alt="image3MA" width=100% />
<img src="  /_image3MD.webp" alt="image3MA" width=100% />


A successful response has status code 200.

What we want to do is start the whole “app part” by listing all the projects in the projects collection in PocketBase.


Go to the PocketBase “Admin UI” URL **http://127.0.0.1:8090/_/**, as we’ve done in Module 1 (restart PocketBase if you stopped its process with **./pocketbase serve** (**.\pocketbase serve** on Windows Powershell) from the folder where you added the PocketBase command, as we did in module 1).

Here is the projects collection we created in module 1:


<img src="../_image3ME.webp" alt="image3MA" width=100% />
<img src="  /_image3ME.webp" alt="image3MA" width=100% />


I want to add some projects here, using the PocketBase interface.

But first we have to add a user. The reason is that each product has a created_by property that links to a user.

So first go to the users collection and add a user by clicking “New record”:


<img src="../_image3MF.webp" alt="image3MA" width=100% />
<img src="  /_image3MF.webp" alt="image3MA" width=100% />

You’ll see a form show up:

<img src="../_image3MG.webp" alt="image3MA" width=100% />
<img src="  /_image3MG.webp" alt="image3MA" width=100% />

Fill the Email and Password fields. Also set Public: On on the email field (see the green text in the screenshot below) — we’ll talk about this later, but basically we’ll use this to be able to search users by email, by default unlocked for privacy reasons.

<img src="../_image3MH.webp" alt="image3MA" width=100% />
<img src="  /_image3MH.webp" alt="image3MA" width=100% />


Click “Create” and you should see the record:

<img src="../_image3MI.webp" alt="image3MA" width=100% />
<img src="  /_image3MI.webp" alt="image3MA" width=100% />


Now select to the projects collection.

Click “New record” and add a few sample projects:


<img src="../_image3MJ.webp" alt="image3MA" width=100% />
<img src="  /_image3MJ.webp" alt="image3MA" width=100% />

Set a name, a status from the list, and pick a user:


<img src="../_image3MK.webp" alt="image3MA" width=100% />
<img src="  /_image3MK.webp" alt="image3MA" width=100% />

Add a few records, just to have some data to visualize:


<img src="../_image3ML.webp" alt="image3MA" width=100% />
<img src="  /_image3ML.webp" alt="image3MA" width=100% />

## Start fetching data from PocketBase

Now we’re ready to fetch the data from PocketBase.

To do this, go to the terminal and install the pocketbase npm package.

This is the first npm package we install. This is how we “import” code that other people created, and we can use in our projects.

Run the command from the folder that contains package.json (the root folder of Astro):

```

npm install pocketbase

```


<img src="../_image3MM.webp" alt="image3MA" width=100% />
<img src="  /_image3MM.webp" alt="image3MA" width=100% />

The entry has been added to the package.json file:


<img src="../_image3MN.webp" alt="image3MA" width=100% />
<img src="  /_image3MN.webp" alt="image3MA" width=100% />


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

<img src="../_image3MO.webp" alt="image3MA" width=100% />
<img src="  /_image3MO.webp" alt="image3MA" width=100% />


## Show the projects list on the page

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

<img src="../_image3MP.webp" alt="image3MA" width=100% />
<img src="  /_image3MP.webp" alt="image3MA" width=100% />


## Create a layout for the app

This method we used to show the projects list is ok, but let’s do it in a different way now.

We’re going to create a lot of screens in the “app” portion of our project, so let’s create a src/layouts/LayoutApp.astro layout - similarly to what we did with src/layouts/LayoutSite.astro for the site part.

```

---
const { title = 'Secretplan' } = Astro.props
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

This layout has a title prop, that will be used to fill the <title> tag content.

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

**TIP** Sometimes you may get an error when adding a file to VS Code and then import it. Running **Developer: Restart Extension Host" command in VS Code from the Command Palette (cmd-shift-p OR ctrl-shift-p OR shift-greaterthan key). 

The layout now provides some built-in padding that will be set across all pages in our app:

<img src="../_image3MQ.webp" alt="image3MA" width=100% />
<img src="  /_image3MQ.webp" alt="image3MA" width=100% />


## Show projects nicely

