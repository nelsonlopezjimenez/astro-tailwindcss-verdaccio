---
title: Module 4
date: 2024-01-20
---

In module 4 we'll first add a sidebar that lists all
projects, with a hamburger menu to show it on mobile too.
We'll use htmx's `hx-boost` feature to make the app feel
faster. Then we'll add a way to mark tasks as done, edit the
project status, edit the project's name, and edit the task
text. We'll also add a way to delete a project and a task.
We'll add the ability to "star" a task, and we'll then show
starred tasks coming form all projects in the dashboard

# Content

1. Introduction to the module
2. Add a sidebar
3. List projects in the sidebar
4. Add hamburger menu to show projects list on mobile
5. Add x-cloak to prevent flicker
6. Moving styles to app.css
7. Use hx-boost to smooth navigation
8. Sort projects by status
9. Fix the TS errors
10. Use the logo font for the pages title
11. Delete a project
12. Allow to edit the project status
13. Let people edit the project’s name.
14. Delete a task
15. Add a way to mark tasks as done
16. Show “done” tasks in a different list
17. Star a task
18. Show starred tasks in the dashboard
19. Edit the task text
20. Wrapping up

In module 3 we started working on the “app” part.

We’ve seen how to fetch data from PocketBase from Astro, and how
to insert data.

Then we’ve seen how to use htmx and Alpine for simple needs.

In this module we’ll keep adding interactivity and data management
features to our app.

We’ll implement a sidebar, where we’ll list the projects found in
PocketBase.

Then we’ll allow people to delete a project, edit its status and
name.

We’ll let people delete a task, mark tasks as done, star a task,
and edit the task text, and more!

## Add a sidebar

Let’s add a sidebar so people can navigate easily between
projects, but also easily go back to the dashboard.

Create the file **src/components/app/Sidebar.astro** and add this
content to it:

```

<aside class='text-white'>
   <div class='mb-6 rounded-lg bg-zinc-800'>
      <div class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 textxl sm:text-2xl md:text-3xl text-white uppercase text-center
font-extrabold'>
<a href='/app/dashboard'>SPRING24APP</a>
      </div>
   </div>
</aside>

```

Now we’re going to include this component in
src/layouts/LayoutApp.astro :

```

---
import Sidebar from '@components/app/Sidebar.astro'
//...
---
...
<body x-data>
<main
class='min-h-screen dark:bg-black dark:text-white'>
<div class='max-w-5xl px-4 py-4 mx-auto'>
<dialog></dialog>
<slot />
<div class='flex sm:space-x-6'>
<div class='hidden w-1/3 sm:block'>
<Sidebar />
</div>
<div class='w-full sm:w-2/3'>
<slot />
</div>
</div>
</div>
</main>
</body>
...
```

4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 1/104
Module 4
In module 4 we'll first add a sidebar that lists all
projects, with a hamburger menu to show it on mobile too.
We'll use htmx's `hx-boost` feature to make the app feel
faster. Then we'll add a way to mark tasks as done, edit the
project status, edit the project's name, and edit the task
text. We'll also add a way to delete a project and a task.
We'll add the ability to "star" a task, and we'll then show
starred tasks coming form all projects in the dashboard.
1: Introduction to the module
2: Add a sidebar
3: List projects in the sidebar
4: Add hamburger menu to show projects list on mobile
5: Add x-cloak to prevent flicker
6: Moving styles to app.css
7: Use hx-boost to smooth navigation
8: Sort projects by status
9: Fix the TS errors
10: Use the logo font for the pages title
11: Delete a project
12: Allow to edit the project status
13: Let people edit the project’s name.
14: Delete a task
15: Add a way to mark tasks as done
16: Show “done” tasks in a different list
17: Star a task
18: Show starred tasks in the dashboard
19: Edit the task text
20: Wrapping up
[← back to all the Bootcamp modules]
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 2/104

<aside class='text-white'>
<div class='mb-6 rounded-lg bg-zinc-800'>
<div
In module 3 we started working on the “app” part of the bootcamp.
We’ve seen how to fetch data from PocketBase from Astro, and how
to insert data.
Then we’ve seen how to use htmx and Alpine for simple needs.
In this module we’ll keep adding interactivity and data management
features to our app.
We’ll implement a sidebar, where we’ll list the projects found in
PocketBase.
Then we’ll allow people to delete a project, edit its status and
name.
We’ll let people delete a task, mark tasks as done, star a task,
and edit the task text, and more!
NOTE: find the full code of this module on
https://github.com/flaviocopes/bootcamp-2024/tree/mod4
Adda sidebar
Let’s add a sidebar so people can navigate easily between
projects, but also easily go back to the dashboard.
Create the file src/components/app/Sidebar.astro and add this
content to it:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 3/104
class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 textxl sm:text-2xl md:text-3xl text-white uppercase text-center
font-extrabold'>
<a href='/app/dashboard'>SECRETPLAN</a>
</div>
</div>
</aside>
---
import Sidebar from '@components/app/Sidebar.astro'
//...
---
...
<body x-data>
<main
class='min-h-screen dark:bg-black dark:text-white'>
<div class='max-w-5xl px-4 py-4 mx-auto'>
<dialog></dialog>
<slot />
<div class='flex sm:space-x-6'>
<div class='hidden w-1/3 sm:block'>
<Sidebar />
</div>
<div class='w-full sm:w-2/3'>
<slot />
</div>
</div>
</div>
</main>
</body>
...
Now we’re going to include this component in
src/layouts/LayoutApp.astro :
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 4/104
---
//...
---
<LayoutApp title='Dashboard'>
<div class='py-10 mx-auto text-white max-w-7xl space-y-6'>
<div class='mx-auto text-white max-w-7xl space-y-6'>
<div
class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 textxl sm:text-3xl md:text-5xl text-white uppercase text-center
font-extrabold'
REMINDER: lines underline in red mean “remove this line”. Green
lines mean “add this line”
Here’s what you should see:
Let me adjust how the “projects” heading element looks like, so
it’s “on par” with the sidebar heading.
In src/pages/app/dashboard.astro :
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 5/104
class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 textxl sm:text-2xl md:text-3xl text-white uppercase text-center
font-extrabold'
>
Projects
</div>
...
Let’s also fix the single project view:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 6/104
---
//...
---
<LayoutApp title={project.name}>
<div class='py-10 mx-auto text-white max-w-7xl space-y-6'>
<div class='mx-auto text-white max-w-7xl space-y-6'>
<div
class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 textxl sm:text-3xl md:text-5xl text-white uppercase text-center
font-extrabold'
class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 textxl sm:text-2xl md:text-3xl text-white uppercase text-center
font-extrabold'
>
{project.name}
</div>
...
In src/pages/app/project/[project_id].astro :
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 7/104
Here’s the result so far, with sidebar and main content well
aligned:
Note that on smaller screens, the sidebar is not visible thanks to
the Tailwind CSS classes we used in the markup:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 8/104
---
import { getProjects } from '@data/pocketbase'
const projects = await getProjects()
---
<aside class='text-white'>
<div class='mb-6 rounded-lg bg-zinc-800'>
<div
class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 textxl sm:text-2xl md:text-3xl text-white uppercase text-center
font-extrabold'>
<a href='/app/dashboard'>SECRETPLAN</a>
</div>
</div>
<div class='mb-6 rounded-lg bg-zinc-800'>
<a
href='/app/dashboard'
class={'block bg-zinc-900 py-2 pl-2 cursor-pointer
hover:bg-zinc-800 border-b border-zinc-800 uppercase bordert-zinc-400 font-black rounded-t-lg ' +
(projects.length === 0 ? ' rounded-b-lg ' : '') +
(Astro.url.pathname === '/app/dashboard' &&
' font-bold !bg-blue-800 ') +
(Astro.params.project_id &&
So to see the sidebar, make the window larger (we’ll add a way to
see the sidebar content on smaller screens later).
Listprojects inthesidebar
Now let’s list the projects we currently have in PocketBase in the
sidebar.
Add this to src/components/app/Sidebar.astro :
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 9/104
' !bg-white text-black border ')}>
Your projects
</a>
<div>
{
projects.map((project, index) => {
return (
<a
href={`/app/project/${project.id}`}
class={
'bg-zinc-900 py-2 pl-2 cursor-pointer
hover:bg-zinc-800 border-b border-zinc-800' +
(Astro.url.pathname ===
`/app/project/${project.id}`
? ' font-bold !bg-blue-800'
: '') +
(index === projects.length - 1
? ' rounded-b-lg '
: '') +
' flex justify-between'
}>
<span>{project.name}</span>
<span class='mr-2'>
{Astro.url.pathname ===
`/app/project/${project.id}` && (
<span>▶︎</span>
)}
</span>
</a>
)
})
}
</div>
</div>
</aside>
Since we now call getProjects() in 2 different places in the
same page, we also need to do one thing.
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 10/104
We need to tell PocketBase to disable auto cancellation, which is
something the PocketBase JavaScript SDK does to cancel duplicated
requests (see https://github.com/pocketbase/jssdk/blob/master/README.md#auto-cancellation to read more),
otherwise we’d see errors like this:
and this error in the terminal:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 11/104
import PocketBase from 'pocketbase'
export const pb = new PocketBase(
import.meta.env.POCKETBASE_URL ||
process.env.POCKETBASE_URL
)
// globally disable auto cancellation
pb.autoCancellation(false)
To prevent this, open src/data/pocketbase.ts and at the top of
the file add pb.autoCancellation(false) :
This will prevent the error from appearing. Auto cancellation
might be a useful feature but we don’t need this to build our MVP
(minimum viable product), and in my humble opinion should be
disabled by default, but we got to do this manually now.
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 12/104
That said, let’s go back to the snippet of code we added above to
the sidebar.
We added some logic to check if the current URL (which you get via
Astro.url.pathname ) corresponds to the project URL, and in this
case we add some visual styling to indicate we’re watching that
specific project.
Same logic to detect if we’re on the dashboard page.
Here’s the result on the dashboard:
You can now select a project in the sidebar, or from the dashboard
content, and you’ll go to the project detail page, with the
current project highlighted:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 13/104
Addhamburgermenutoshow projects listonmobile
Let’s now make the sidebar appear on mobile screens, so we have
nice navigation on smaller screens too.
To do so, we declare an Alpine data variable showMenu
initialized to false by using the x-data='{showMenu : false}'
attribute on a div .
Read more about this kind of approach in
https://thevalleyofcode.com/alpine/4-define-data.
This variable will now be available inside this div and all its
child elements.
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 14/104
...
<body>
<body x-data>
<main
class='min-h-screen dark:bg-black dark:text-white'>
<div class='max-w-5xl px-4 py-4 mx-auto'>
<dialog></dialog>
<div class='flex sm:space-x-6'>
<div class='hidden w-1/3 sm:block'>
<Sidebar />
</div>
<div class='w-full sm:w-2/3'>
<slot />
</div>
<div
class='w-full sm:w-2/3'
x-data='{showMenu : false}'>
<div x-show='showMenu'>
<Sidebar />
</div>
<slot />
</div>
</div>
</div>
</main>
</body>
...
If this variable is true we show the sidebar component before
the page main content in src/layouts/LayoutApp.astro using the
x-show Alpine directive (https://alpinejs.dev/directives/show):
We need a way to set this variable to true.
We’ll do this by adding a “hamburger” icon near the page title,
and clicking that will set the showMenu variable to true .
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 15/104
<button
aria-label='Show sidebar'
x-show='!showMenu'
@click='showMenu = !showMenu'
class='absolute flex justify-between float-left py-2 pl-2 -
mt-1 text-white bg-blue-500 rounded-lg cursor-pointer'>
<svg
class='w-5 h-5 mr-2'
fill='none'
stroke-linecap='round'
stroke-linejoin='round'
stroke-width='2'
viewBox='0 0 24 24'
stroke='currentColor'>
<path d='M4 6h16M4 12h16M4 18h16'></path>
</svg>
</button>
---
//...
import HamburgerMenuButton from
'@components/app/HamburgerMenuButton.astro'
//...
---
Create src/components/app/HamburgerMenuButton.astro :
Using x-show='!showMenu' we show this only if showMenu is
false.
Then when this is clicked, we set showMenu to true with
@click='showMenu = true'
Include this in src/pages/app/dashboard.astro :
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 16/104
...
<div
class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 textxl sm:text-2xl md:text-3xl text-white uppercase text-center
font-extrabold'>
<div class='sm:hidden'>
<HamburgerMenuButton />
</div>
Projects
</div>
---
//...
import HamburgerMenuButton from
'@components/app/HamburgerMenuButton.astro'
//...
---
...
<div
class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 textxl sm:text-2xl md:text-3xl text-white uppercase text-center
font-extrabold'>
<div class='sm:hidden'>
<HamburgerMenuButton />
</div>
{project.name}
</div>
and in src/pages/app/project/[project_id].astro :
This hamburger button should now be visible when the page is small
enough to make the sidebar disappear:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 17/104
Click it, the sidebar’s content should now appear at the top of
the page:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 18/104
This is all client-side logic (everything happens inside the
browser). Alpine.js made this very simple because it’s all inside
attributes in our HTML, without having to write any custom
JavaScript to interact with the DOM elements.
Now let’s add a button that allows us to also close the menu after
we’ve opened it.
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 19/104
We’ll add it directly to the sidebar, so the “close button” will
appear in the same exact place as the hamburger menu we used to
open it.
In src/components/app/Sidebar.astro add those lines in green:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 20/104
---
import { getProjects } from '@data/pocketbase'
const projects = await getProjects()
---
<aside class='text-white'>
<div class='mb-6 rounded-lg bg-zinc-800'>
<div
class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 textxl sm:text-2xl md:text-3xl text-white uppercase text-center
font-extrabold'>
<button
aria-label='Hide sidebar'
@click.prevent='showMenu = false'
class='sm:hidden absolute flex justify-between floatleft py-2 pl-2 -mt-1 text-white bg-blue-500 rounded-lg
cursor-pointer'>
<svg
class='w-5 h-5 mr-2'
fill='none'
stroke-linecap='round'
stroke-linejoin='round'
stroke-width='2'
viewBox='0 0 24 24'
stroke='currentColor'>
<path d='M6 18L18 6M6 6l12 12'></path>
</svg>
</button>
<a href='/app/dashboard'>SECRETPLAN</a>
</div>
</div>
...
Here’s the result:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 21/104
Addx-cloaktopreventflicker
We have one problem, if you try reloading the window, you’ll see
some flickering issue when in “mobile view”: the modal is still
visible before Alpine.js is loaded to hide it:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 22/104
<style>
dialog::backdrop {
background-color: rgba(0, 0, 0, 0.7);
backdrop-filter: blur(3px);
I’m sure you can notice this in your version of the app too.
To fix this, we use the x-cloak attribute provided by Alpine.js.
This attribute will take care of this specific problem.
Read more about it here: https://alpinejs.dev/directives/cloak
Add this snippet of CSS to the <style> tag in
src/layouts/LayoutApp.astro :
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 23/104
}
[x-cloak] {
/* fix alpine js flicker on load */
display: none;
}
</style>
<body x-data>
<main
class='min-h-screen dark:bg-black dark:text-white'>
<div class='max-w-5xl px-4 py-4 mx-auto'>
<dialog></dialog>
<div class='flex sm:space-x-6'>
<div class='hidden w-1/3 sm:block'>
<Sidebar />
</div>
<div
class='w-full sm:w-2/3'
x-data='{showMenu : false}'>
<div x-show='showMenu'>
<div x-show='showMenu' x-cloak>
<Sidebar />
</div>
<slot />
</div>
</div>
</div>
</main>
</body>
And add the x-cloak attribute to the sidebar container div
This solved the problem we had, there is no flickering any more!
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 24/104
@tailwind base;
@tailwind components;
@tailwind utilities;
dialog::backdrop {
background-color: rgba(0, 0, 0, 0.7);
backdrop-filter: blur(3px);
}
[x-cloak] {
/* fix alpine js flicker on load */
display: none;
}
Movingstyles toapp.css
We just added some CSS style into LayoutApp.astro , and it’s
completely fine if we just have a few lines of CSS.
But even though we use Tailwind CSS, which helps us style our
pages using classes in our HTML / templates, I imagine we’re going
to have some bits of CSS we’ll need to add to customize things.
So, as we did for the site part with src/site.css , let’s create
a dedicated app.css file.
Create the file src/app.css and add this content:
Now remove the <style> tag in src/layouts/LayoutApp.astro
which contained those 2 rules we now moved to the CSS file.
Then add this line at the top of src/layouts/LayoutApp.astro to
import the CSS file:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 25/104
import '@src/app.css'
---
import '@src/app.css'
import Sidebar from '@components/app/Sidebar.astro'
const { title = 'Secretplan' } = Astro.props
---
<html lang='en'>
<head>
<meta charset='utf-8' />
<link rel='icon' type='image/svg+xml' href='/favicon.svg'
/>
<meta name='viewport' content='width=device-width' />
<title>{title}</title>
<meta name='description' content='A project management
tool' />
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
This should be the full code of src/layouts/LayoutApp.astro at
this point:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 26/104
htmx.process(document.body)
</script>
</head>
<body x-data>
<main class='min-h-screen dark:bg-black dark:text-white'>
<div class='max-w-5xl px-4 py-4 mx-auto'>
<dialog></dialog>
<div class='flex sm:space-x-6'>
<div class='hidden w-1/3 sm:block'>
<Sidebar />
</div>
<div class='w-full sm:w-2/3' x-data='{showMenu :
false}'>
<div x-show='showMenu' x-cloak>
<Sidebar />
</div>
<slot />
</div>
</div>
</div>
</main>
</body>
</html>
Use hx-boost tosmoothnavigation
Now if you switch between projects in the sidebar, you’ll see the
page flickering a little bit because the browser does a full page
reload on every link click.
This is a different issue than the one we solved above with xcloak .
This issue is related to how our web application works.
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 27/104
It’s essential to look at the Browser DevTools Network tab (see
https://flaviocopes.com/browser-dev-tools/) and see what happens
when you click a link, everything gets requested from the server
again on each link click:
This is what happens by default in the Web browser when you click
a link to another page.
It’s not exactly bad per se, it works, but you can improve this
and provide a smoother navigation experience, to make it feel more
similar to mobile apps or other cool web applications you use
every day.
I think we have 2 ways here.
The first is using Astro View Transitions. It’s a very cool
feature offered by Astro out of the box:
https://docs.astro.build/en/guides/view-transitions/ and basically
by default when you enable them Astro will preload a page when you
go over the link with the mouse, and will then have a nice CSS
transition to the new content when the link is eventually clicked.
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 28/104
<body x-data>
<body x-data hx-boost='true'>
This is a big perceived performance improvement over the default
behavior of the browser.
The other option is to enable Boost Mode in htmx.
Boost mode can be enabled by just adding an attribute to the body:
hx-boost .
This is an htmx feature that basically requests the page, but
instead of letting the browser do the usual request/response
handling, it gets the page using AJAX, adds the content of the
page returned to the innerHTML of the body, basically doing what
htmx always does (swapping HTML partials) but applied to the whole
body, and by default to all links (and forms).
Add hx-boost="true" to the body tag in
src/layouts/LayoutApp.astro , like this:
Navigation gets a lot smoother now, and things are much faster
too.
And it’s actually faster, not just perceived to be faster, as you
can see in the Network panel of the DevTools:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 29/104
Sortprojectsbystatus
Right now projects are sorted, both in the dashboard and in the
sidebar, by date: the first created is first, and if we add a new
one, it’s listed last.
Let’s change this ordering to order projects by status.
We’ll put first projects that are completed, then we’ll have the
ones “ongoing”, which means they don’t have a clear end (think a
blog, for example).
Then we’ll order by:
almost finished
in progress
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 30/104
export async function getProjects() {
const projects = await pb
.collection('projects')
.getFullList()
return projects
}
started
on hold (projects currently blocked or suspended)
not started
You can decide your own ordering, but this is what we’ll
implement.
We fetch projects using getProjects() defined in
/src/data/pocketbase.ts .
Let’s go in there and change the ordering.
The function is currently defined as:
We can change it to sort projects before returning projects to
whoever calls it.
We could also ask PocketBase to return items in a particular
order. If the way we order them was by title, perhaps. But in our
case, we order by this property in a semi-random way.
I could have “hardcoded” the order in the database, using status
values like 2-ongoing , 3-almost-finished , etc, but I think
this way gives us more flexibility.
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 31/104
function getStatus(project) {
switch (project.status) {
case "not started":
return 7;
case "on hold":
return 6;
case "started":
return 5;
case "in progress":
return 4;
case "almost finished":
return 3;
case "ongoing":
return 2;
case "done":
return 1;
default:
return 0;
}
}
export async function getProjects() {
const projects = await pb
.collection('projects')
.getFullList()
return projects
return projects.sort(
Create a getStatus() function, we’ll use it to associate a
status with a number:
(ignore the errors highlighted by VS Code, for now)
Then we’ll use this function in the sort() callback function
used to order:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 32/104
(a, b) => getStatus(a) - getStatus(b)
)
}
src/data/pocketbase.ts:18:29 - error ts(7006): Parameter 'proj
18 function getStatus(project) {
Now projects will be ordered by status.
NOTE: if you get an error, try moving the getStatus() function
definition “up” in the file, so it’s defined before you use it
Fix the TSerrors
As you implemented getStatus() , if you noticed we got an error,
which might be visible in VS Code, or also by running the command
npm run astro check from the terminal, a built-in Astro command
we can use to check for TypeScript errors in the terminal:
Basically, TypeScript cannot determine the type of the project
variable passed to getStatus() .
To fix this we’re going to add types for our PocketBase data
collections.
PocketBase does not have built-in types support, but we’ll use the
tool https://github.com/patmood/pocketbase-typegen to generate our
types.
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 33/104
pocketbase/
app/
npx pocketbase-typegen --db ../pocketbase/pb_data/data.db --ou
We have to go to the terminal and run a command.
I assume you have created a folder structure like this for your
project:
or something similar.
The names of the folders don’t matter but basically, pocketbase
should be on the same level of your app folder.
If you created app inside the pocketbase folder, as I’ve seen
some do, please move app outside of that folder - they are 2
separate things and should be kept separate, also for an easier
deployment later on.
The command below assumes you are inside the “app” folder with the
terminal, so the pb_data folder of PocketBase is found at
../pocketbase/pb_data . If this is not the case, change the path
accordingly:
NOTE: if you use PocketHost, or host PocketBase in the cloud in
other ways, you must connect to that instance, there is
documentation of how to do this on
https://github.com/patmood/pocketbase-typegen?tab=readme-ovfile#usage - for example with a test PocketHost site I used npx
pocketbase-typegen --url https://MYSUBDOMAIN.pockethost.io --
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 34/104
/**
* This file was @generated using pocketbase-typegen
*/
import type PocketBase from 'pocketbase'
import type { RecordService } from 'pocketbase'
export enum Collections {
Projects = "projects",
Tasks = "tasks",
Users = "users",
}
// Alias types for improved usability
export type IsoDateString = string
export type RecordIdString = string
export type HTMLString = string
// System fields
export type BaseSystemFields<T = never> = {
id: RecordIdString
created: IsoDateString
updated: IsoDateString
collectionId: string
collectionName: Collections
expand?: T
}
export type AuthSystemFields<T = never> = {
email: string
emailVisibility: boolean
username: string
email my@email.com --password 'mypassword' --out
./src/data/pocketbase-types.ts (change your subdomain, email and
password of course)
After running the command you’ll find a new file generated in
src/data/pocketbase-types.ts , like this one:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 35/104
verified: boolean
} & BaseSystemFields<T>
// Record types for each collection
export enum ProjectsStatusOptions {
"not started" = "not started",
"started" = "started",
"in progress" = "in progress",
"almost finished" = "almost finished",
"done" = "done",
"ongoing" = "ongoing",
"on hold" = "on hold",
"archived" = "archived",
}
export type ProjectsRecord = {
created_by?: RecordIdString
name?: string
status?: ProjectsStatusOptions
}
export type TasksRecord = {
completed?: boolean
completed_on?: IsoDateString
created_by?: RecordIdString
images?: string[]
project: RecordIdString
starred?: boolean
starred_on?: IsoDateString
text?: string
}
export type UsersRecord = {
avatar?: string
name?: string
}
// Response types include system fields and match responses from
export type ProjectsResponse<Texpand = unknown> = Required<Pro
export type TasksResponse<Texpand = unknown> = Required<TasksR
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 36/104
export type UsersResponse<Texpand = unknown> = Required<UsersR
// Types containing all Records and Responses, useful for creati
export type CollectionRecords = {
projects: ProjectsRecord
tasks: TasksRecord
users: UsersRecord
}
export type CollectionResponses = {
projects: ProjectsResponse
tasks: TasksResponse
users: UsersResponse
}
// Type for usage with type asserted PocketBase instance
// https://github.com/pocketbase/js-sdk#specify-typescript-defin
export type TypedPocketBase = PocketBase & {
collection(idOrName: 'projects'): RecordService<ProjectsResp
collection(idOrName: 'tasks'): RecordService<TasksResponse>
collection(idOrName: 'users'): RecordService<UsersResponse>
}
import type {
TypedPocketBase,
ProjectsResponse,
} from '@src/data/pocketbase-types'
Now we’ll add this snippet of code at the top of
src/data/pocketbase.ts :
We then change how we initialize PocketBase by setting the type of
the pb variable to TypedPocketBase :
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 37/104
export const pb = new PocketBase(
import.meta.env.POCKETBASE_URL ||
process.env.POCKETBASE_URL
)
) as TypedPocketBase
function getStatus(project) {
function getStatus(project: ProjectsResponse) {
After this, we’ll be able to set the type of the project
attribute we pass to the getStatus function:
Now you should not have any TypeScript error in this file anymore.
Note: we’ll have to re-run the npx pocketbase-typegen command we
used above any time we edit the collections, as they are not kept
in sync automatically.
It’s a small inconvenience, for a good benefit (having hints and
type checking that will keep us on the right track).
Usethelogofontfor thepages title
In the homepage, we used a logo I provided you, which used a nice
font:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 38/104
Now I want to use this font in the app part too:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 39/104
npm install @fontsource/m-plus-rounded-1c
---
//...
import '@fontsource/m-plus-rounded-1c'
import '@fontsource/m-plus-rounded-1c/800.css'
---
.font-rounded {
font-family: 'M PLUS Rounded 1c', sans-serif;
}
To do this, I’m going to use Fontsource, a service I found in
Astro’s documentation about fonts.
This service simplifies including custom fonts, and in particular
Google Fonts, and the font I used in the SVG logo was “M PLUS
Rounded 1c”: https://fonts.google.com/specimen/M+PLUS+Rounded+1c
To include it in our site, first install it:
Then in LayoutApp.astro you include it at the top:
then you can use it in your CSS in src/app.css :
Ok, now we can apply the font-rounded class to any element we
want to use this font.
In particular in src/pages/app/dashboard.astro :
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 40/104
//...
<LayoutApp title='Dashboard'>
<div class='mx-auto text-white max-w-7xl space-y-6'>
<div
class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 text-x
class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 text-x
<div class='sm:hidden'>
<HamburgerMenuButton />
</div>
Projects
</div>
//...
//...
<LayoutApp title={project.name}>
<div class='mx-auto text-white max-w-7xl space-y-6'>
<div
class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 textxl sm:text-2xl md:text-3xl text-white uppercase text-center
font-extrabold'>
class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 textxl sm:text-2xl md:text-3xl text-white uppercase text-center
font-extrabold font-rounded'>
//...
---
import { getProjects } from '@data/pocketbase'
and src/pages/app/project/[project_id].astro :
and src/components/app/Sidebar.astro :
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 41/104
const projects = await getProjects()
---
<aside class='text-white'>
<div class='mb-6 rounded-lg bg-zinc-800'>
<div
class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 textxl sm:text-2xl md:text-3xl text-white uppercase text-center
font-extrabold'>
class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 textxl sm:text-2xl md:text-3xl text-white uppercase text-center
font-extrabold font-rounded'>
Here’s the result:
Looks much better!
Deleteaproject
Let’s now add a new panel in the project page to allow us to
delete a project.
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 42/104
<button
hx-delete={`/app/api/project/${project_id}`}
>
Delete project
</button>
<button
hx-delete={`/app/api/project/${project_id}`}
hx-confirm='Are you sure?'
>
Delete project
</button>
We’ll add a button that when clicked will send a DELETE HTTP
request to the URL /app/api/project/<project_id> .
We do this using htmx, by passing the URL we want to “trigger”
with the hx-delete attribute:
This is all we have to do to make a HTTP DELETE network request to
the server, to the specified endpoint. As a reminder, check out
https://flaviocopes.com/http/ to see how HTTP requests work.
Since this is a destructive action, we can also add a hx-confirm
attribute to the element, to make the user confirm the action
(this is something provided to us by htmx - see
https://htmx.org/attributes/hx-confirm/):
We add this, with some classes to style it, to
src/pages/app/project/[project_id].astro .
We also wrap it in a container div:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 43/104
---
import LayoutApp from '@layouts/LayoutApp.astro'
import { getProject, getTasks } from '@data/pocketbase'
import ButtonAddNewTask from
'@components/app/tasks/ButtonAddNewTask.astro'
import HamburgerMenuButton from
'@components/app/HamburgerMenuButton.astro'
const { project_id } = Astro.props
const project = await getProject(project_id)
if (!project) {
return Astro.redirect('/app/dashboard')
}
const tasks = await getTasks(project_id)
---
<LayoutApp title={project.name}>
<div class='mx-auto space-y-6 text-white max-w-7xl'>
<div
class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 textxl sm:text-2xl md:text-3xl text-white uppercase text-center
font-rounded font-extrabold'>
<div class='sm:hidden'>
<HamburgerMenuButton />
</div>
{project.name}
</div>
<div class='space-y-6'>
<div
class='p-10 text-white rounded-lg shadow bg-zinc-100
dark:bg-zinc-800'>
<h2
class='pb-10 text-xl font-black text-center
uppercase text-zinc-800 dark:text-white'>
Tasks to do
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 44/104
</h2>
<div>
{
tasks.length === 0 && (
<p class='text-center text-zinc-900 dark:textwhite'>Nothing yet</p>
)
}
<ul class='space-y-6'>
{tasks.map(task => <li>{task.text}</li>)}
</ul>
</div>
<ButtonAddNewTask project_id={project_id} />
</div>
<div
class='p-10 text-white rounded-lg shadow bg-zinc800'>
<h2
class='pb-0 text-xl font-black text-center
uppercase font-rounded'>
Danger zone
</h2>
<div class='w-full mx-auto text-center'>
<button
hx-delete={`/app/api/project/${project_id}`}
hx-confirm='Are you sure?'
class='px-3 py-2 mx-auto mt-5 mr-2 text-sm fontmedium leading-4 text-white border border-transparent
rounded-md shadow-sm bg-zinc-600 hover:bg-red-700
focus:outline-none focus:ring-2 focus:ring-offset-2
focus:ring-red-500'>
Delete project
</button>
</div>
</div>
</div>
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 45/104
</div>
</LayoutApp>
export async function deleteProject(id: string) {
await pb.collection('projects').delete(id)
}
Here’s the result:
Let’s handle the API side now, that’s where we’ll make the magic
happen (in other words, where we’ll actually delete the project by
calling the PocketBase API).
First we add a function to src/data/pocketbase.ts to delete a
project:
Then we create the src/pages/app/api/project/[project_id].astro
file, that will handle the DELETE HTTP request coming from the
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 46/104
---
export const partial = true
import { deleteProject } from '@data/pocketbase'
const { project_id } = Astro.params
if (!project_id) {
return new Response(null, {
status: 400,
statusText: 'Bad Request',
})
}
if (Astro.request.method === 'DELETE') {
await deleteProject(project_id)
return new Response(null, {
status: 204,
statusText: 'No Content',
headers: {
'HX-Redirect': '/app/dashboard',
},
})
}
---
page:
In this file we basically say this is a “partial”, like we do for
all API pages (see https://docs.astro.build/en/basics/astropages/#page-partials). This is necessary so the output generated
by Astro will be “clean”, because if you omit the first line,
Astro will return a html tag as it thinks this is a complete web
page, while in reality it’s not.
We don’t want to return anything from this partial.
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 47/104
Then we import deleteProject() , we get the project_id from the
route parameters (thanks to the file structure we use, we have a
dynamic parameter set by the route - the URL in other words).
Is there’s no project_id value, we return a 400 response saying
there’s an error. But if we do, and the HTTP request method is
DELETE , we delete the project and return a successful response
with status 204 (which means “ok, but we don’t return anything”).
The HX-Redirect HTTP header we pass to the response will make
htmx redirect to the URL we pass. It’s a bit of magic that htmx
provides for us, and it’s an awesome way to build our app
experience. See https://flaviocopes.com/htmx-redirect-afterrequest/
If you see an error like this in VS Code:
From the command palette of VS Code (View -> Command Palette) run
“Developer: Restart Extension Host”
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 48/104
The error should disappear (remember this, as similar errors might
happen from time to time). It’s not really an application error,
just some TypeScript / VS Code sync issue.
Ok, so now you can delete a project by clicking the button we just
implemented.
Try it! The project will be deleted and you’ll be sent back to the
dashboard, as we told htmx to do.
Since we set in PocketBase to “Cascade delete” all tasks when
deleting a project, in module 1, tasks when a project is deleted,
all projects tasks will be deleted from the database as well (this
will keep the table cleaner automatically).
Allow toedittheproject status
Let’s now allow people to edit the project’s current status.
First we add a <select> element where we list the statuses a
project can have, which we default to the current active status.
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 49/104
---
const { project } = Astro.props
---
<style>
.select-custom-arrow-icon {
background-image: url('data:image/svg+xml;charset=USASCII,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24
24" fill="%23000"><path d="M7 10l5 5 5-5z"></path></svg>');
/* SVG arrow */
background-repeat: no-repeat;
background-position: right 0 center; /* Adjust as needed
*/
background-size: 1.5rem; /* Adjust as needed */
}
@media (prefers-color-scheme: dark) {
.select-custom-arrow-icon {
background-image: url('data:image/svg+xml;charset=USASCII,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24
24" fill="%23fff"><path d="M7 10l5 5 5-5z"></path></svg>');
}
}
</style>
<select
aria-label='Change project status'
class='w-full h-8 px-4 text-sm border-r-8 bordertransparent rounded appearance-none outlin outline-1 outlineWe list all statuses except “archived” that we’ll reserve for a
dedicated button/action, as it will do a little more than just
changing the state, it will also hide the project from our main
list, and put it in an archive view (we’ll do this later).
Let’s do this in a component we call
src/components/app/projects/ProjectStatus.astro :
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 50/104
neutral-700 select-custom-arrow-icon focus:ring-offset-0
dark:bg-zinc-900 text-zinc-800 dark:text-white'
name='status'
value={project.status}
hx-put={`/app/api/project/${project.id}`}
hx-swap='none'
hx-trigger='change'
hx-vals=`{"action": "change_status"}`>
<option
value='not started'
selected={project.status === 'not started' &&
'selected'}>
not started
</option>
<option
value='on hold'
selected={project.status === 'on hold' && 'selected'}>
on hold
</option>
<option
value='started'
selected={project.status === 'started' && 'selected'}>
started
</option>
<option
value='in progress'
selected={project.status === 'in progress' &&
'selected'}>
in progress
</option>
<option
value='ongoing'
selected={project.status === 'ongoing' && 'selected'}>
ongoing
</option>
<option
value='almost finished'
selected={project.status === 'almost finished' &&
'selected'}>
almost finished
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 51/104
</option>
<option
value='done'
selected={project.status === 'done' && 'selected'}>
done
</option>
</select>
---
//...
import ProjectStatus from
'@components/app/projects/ProjectStatus.astro'
---
//...
<LayoutApp title={project.name}>
<div class='mx-auto space-y-6 text-white max-w-7xl'>
<div
class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 textxl sm:text-2xl md:text-3xl text-white uppercase text-center
font-rounded font-extrabold'>
<div class='sm:hidden'>
<HamburgerMenuButton />
</div>
{project.name}
Notice I used a custom CSS class called select-custom-arrow-icon
to customize the select.
Astro <style> CSS rules are automatically scoped by default.
This means they only apply to HTML written inside of that same
component.
We include this component in
src/pages/app/project/[project_id].astro , along with a link to
the dashboard:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 52/104
</div>
<div
class='flex items-center justify-between mx-auto max-w7xl'>
<a href={'/app/dashboard'}>
<button
type='button'
class='text-xl btn-header text-zinc-800 dark:textwhite'>
◀︎ All your projects
</button>
</a>
<div class='mr-0.5'>
<ProjectStatus project={project} />
</div>
</div>
<div class='space-y-6'>
<div
class='p-10 text-white rounded-lg shadow bg-zinc-100
dark:bg-zinc-800'>
<h2
class='pb-10 text-xl font-black text-center
uppercase text-zinc-800 dark:text-white'>
Tasks to do
</h2>
//...
You should see this:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 53/104
import type {
TypedPocketBase,
ProjectsResponse,
ProjectsRecord,
} from '@src/data/pocketbase-types'
When you change the value of the status, htmx issues a PUT request
to /app/api/project/<project_id> sending an action property
with the change_status value.
This happens because we used the hx-trigger attribute to trigger
the PUT request (as we used hx-put ) when the “change” event is
triggered on the select (when we change its value, basically).
The hx-vals htmx attribute lets us also send to the API (in
addition to the value which is sent automatically) an action
parameter, in this case with the value change_status .
We pass an action because we’ll also edit the project record later
to change its name, so we need a way to recognize what we’re
editing.
Now we add an updateProject method to src/data/pocketbase.ts
(we also import the ProjectsRecord type):
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 54/104
//...
export async function updateProject(
id: string,
data: ProjectsRecord
) {
await pb.collection('projects').update(id, data)
}
---
export const partial = true
import {
deleteProject,
updateProject,
} from '@data/pocketbase'
import { ProjectsStatusOptions } from '@data/pocketbasetypes'
const { project_id } = Astro.params
if (!project_id) {
return new Response(null, {
status: 400,
statusText: 'Bad Request',
})
}
if (Astro.request.method === 'DELETE') {
await deleteProject(project_id)
return new Response(null, {
status: 204,
statusText: 'No Content',
and we use this function in
src/pages/app/api/project/[project_id].astro :
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 55/104
headers: {
'HX-Redirect': '/app/dashboard',
},
})
}
if (Astro.request.method === 'PUT') {
const formData = await Astro.request.formData()
const action = formData.get('action')
if (action === 'change_status') {
let status = formData.get('status')
if (status) {
await updateProject(project_id, {
status:
ProjectsStatusOptions[
status as keyof typeof ProjectsStatusOptions
],
})
} else {
return new Response(
'Need to set "status" parameter',
{ status: 400 }
)
}
} else {
return new Response('Invalid action', { status: 400 })
}
}
---
The ProjectsStatusOptions[status as keyof typeof
ProjectsStatusOptions] line is some TypeScript you don’t need to
dive into not and can basically ignore (I want to focus more on
the functionality rather than technicalities like this, and this
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 56/104
is not a TypeScript course), but basically it’s a way to have the
status field typed correctly.
Now you can change the status and the change will be reflected
immediately, as you can notice by going back to the dashboard, or
simply reloading the current page.
Letpeopleedittheproject’sname.
Now let’s add a way to edit a project’s name.
When the user clicks the project name in the project page:
We want to show a modal window like we did previously to create
the project in the first place.
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 57/104
//...
<LayoutApp title={project.name}>
<div class='mx-auto space-y-6 text-white max-w-7xl'>
<div
class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 textxl sm:text-2xl md:text-3xl text-white uppercase text-center
font-rounded font-extrabold'>
<div class='sm:hidden'>
<HamburgerMenuButton />
</div>
{project.name}
<span
hx-get='/app/modals/project/new'
hx-target='dialog'>
{project.name}
</span>
</div>
//...
Let’s start simple by replicating what we did before when we
implemented the modal to add a project.
In src/pages/app/project/[project_id].astro we first wrap the
project name into a span tag that when clicked makes a GET
request to /app/modals/project/new (just a placeholder, we’ll
later use another URL to get the actual content we want to use in
this scenario) to get the modal’s content, and puts it into the
dialog tag (we only have one, so we can use this dialog
selector):
Now if you click the project’s name, this modal should appear:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 58/104
hx-get='/app/modals/project/new'
hx-get=`/app/modals/project/${project.id}/edit`
---
export const partial = true
However this time in the modal we want to display the content that
allows to edit the current project name.
Let’s change the hx-get we just added to this:
(notice I switched from single quote to backticks to enable
interpolating a value using ${} in so-called
https://flaviocopes.com/javascript-template-literals/).
Now create the file
src/pages/app/modals/project/[project_id]/edit.astro
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 59/104
import ModalLayout from
'@components/app/modals/ModalLayout.astro'
import ButtonSubmit from
'@components/app/modals/ButtonSubmit.astro'
import ButtonCancel from
'@components/app/modals/ButtonCancel.astro'
import InputField from
'@components/app/modals/InputField.astro'
const { project_id } = Astro.params
import { getProject } from '@data/pocketbase'
const project = await getProject(project_id!)
---
<ModalLayout title='Edit project name'>
<form
class='space-y-6'
hx-put={`/app/api/project/${project.id}`}
hx-swap='none'
hx-vals=`{"action": "change_name"}`>
<div>
<div class='mt-1'>
<InputField
name='project_name'
value={project.name}
/>
</div>
</div>
<div class='flex justify-center'>
<ButtonSubmit label='Save' />
<ButtonCancel />
</div>
</form>
</ModalLayout>
You should see this happening if you click the project’s name:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 60/104
//...
if (Astro.request.method === 'PUT') {
const formData = await Astro.request.formData()
const action = formData.get('action')
if (action === 'change_status') {
let status = formData.get('status')
if (status) {
await updateProject(project_id, {
status:
ProjectsStatusOptions[
status as keyof typeof ProjectsStatusOptions
],
})
} else {
Now, before saving the new name works, you need to edit
src/pages/app/api/project/[project_id].astro to handle the
change_name action:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 61/104
return new Response(
'Need to set "status" parameter',
{ status: 400 }
)
}
} else if (action === 'change_name') {
const project_name =
formData.get('project_name') as string
if (project_name) {
await updateProject(project_id, {
name: project_name,
})
return new Response(null, {
status: 204,
statusText: 'No Content',
headers: {
'HX-Redirect': '/app/project/' + project_id,
},
})
} else {
return new Response(
'Need to set "project_name" parameter',
{
status: 400,
}
)
}
} else {
return new Response('Invalid action', { status: 400 })
}
}
---
TIP: “as string” is a way to tell TypeScript this is a string
even when the value could be undefined
If the action is change_name now we first get the project_name
value from the form data, then we call updateProject() passing
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 62/104
---
//...
import TasksList from '@components/app/tasks/TasksList.astro'
//...
---
//...
<div>
{
tasks.length === 0 && (
<p class='text-center text-zinc-900 dark:textwhite'>Nothing yet</p>
)
}
the id of the project we want to update, and the new value of the
name.
Finally we return a new 204 response with a HX-Redirect header
to redirect to the project page, so people can immediately see the
new name applied on the page.
You should now be able to edit the project’s name!
Deletea task
Now I want to let people delete a task.
Let’s first create a component to manage the tasks list.
In src/pages/app/project/[project_id].astro replace this block
with a TasksList component:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 63/104
<ul class='space-y-6'>
{tasks.map(task => <li>{task.text}</li>)}
</ul>
</div>
<div id='tasks-todo'>
<TasksList project_id={project_id} />
</div>
import { getProject, getTasks } from '@data/pocketbase'
import { getProject } from '@data/pocketbase'
const tasks = await getTasks(project_id)
---
import { getTasks } from '@data/pocketbase'
const { project_id } = Astro.props
const tasks = await getTasks(project_id)
---
And we remove the getTasks() import and call at the top:
We’re going to offload this to the TasksList component.
Notice I wrapped <TaskList /> in a div tag with an id
attribute.
This is important, because we’ll use this later to update the page
content using a very cool feature of htmx, something that I find
really amazing and will power useful functionality in our app.
Now create src/components/app/tasks/TasksList.astro and in there
we start by adding all the code we removed from
[project_id].astro :
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 64/104
{
tasks.length === 0 && (
<p class='text-center text-zinc-900 dark:textwhite'>Nothing yet</p>
)
}
<ul class='space-y-6 mb-10'>
{tasks.map(task => <li>{task.text}</li>)}
</ul>
<svg
class="w-6 h-6 p-1 text-black rounded-lg hover:bg-red-500
hover:text-white dark:text-white"
fill="none"
stroke="currentColor"
viewBox="0 0 24 24"
xmlns="http://www.w3.org/2000/svg">
<path
stroke-linecap="round"
stroke-linejoin="round"
stroke-width="2"
d="M9 13h6m2 8H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0
01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z">
</path>
</svg>
Everything should work as previously, but now we have abstracted
all the tasks list generation to its own little component.
Create the file src/components/app/icons/IconDelete.astro where
we add a little SVG icon with a bin:
Now create src/components/app/tasks/DeleteTaskButton.astro where
we add a button that shows this image, and when clicked initiates
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 65/104
---
import IconDelete from
'@components/app/icons/IconDelete.astro'
const { task } = Astro.props
---
<button
aria-label='Delete task'
class='focus:ring-red-500 focus:outline-none focus:ring-2
focus:ring-offset-2'
hx-swap='outerHTML'
hx-confirm='Are you sure?'
hx-target='closest li'
hx-delete=
{`/app/api/project/${task.project}/task/${task.id}`}>
<IconDelete />
</button>
---
import { getTasks } from '@data/pocketbase'
import DeleteTaskButton from
'@components/app/tasks/DeleteTaskButton.astro'
const { project_id } = Astro.props
const tasks = await getTasks(project_id)
---
{
tasks.length === 0 && (
<p class='text-center text-zinc-900 dark:textwhite'>Nothing yet</p>
a DELETE HTTP request to
/app/api/project/<PROJECT_ID>/task/<TASK_ID> :
and we add this in src/components/app/tasks/TasksList.astro :
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 66/104
)
}
<ul class='space-y-6'>
{
tasks.map(task => (
<li>
{task.text}
<div class='flex justify-between'>
<div>{task.text}</div>
<div>
<DeleteTaskButton task={task} />
</div>
</div>
</li>
))
}
</ul>
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 67/104
export async function deleteTask(id: string) {
await pb.collection('tasks').delete(id)
}
---
export const partial = true
import { deleteTask } from '@data/pocketbase'
const { task_id = '', project_id = '' } = Astro.params
if (Astro.request.method === 'DELETE') {
Clicking a button will prompt a confirmation, as it’s a
destructive action:
…but nothing else happens, because we haven’t implemented the API
route.
Add this to src/data/pocketbase.ts :
Then create
src/pages/app/api/project/[project_id]/task/[task_id].astro
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 68/104
await deleteTask(task_id)
return new Response(null, { status: 200 })
}
---
<svg
class="w-5 h-5 text-white"
xmlns="http://www.w3.org/2000/svg"
viewBox="0 0 20 20"
fill="currentColor"
aria-hidden="true">
<path
fill-rule="evenodd"
d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414
0z"
This will be the API route called by the delete action.
Now tasks are deleted, and when this happens, the element is
removed from the page.
Note that the route we created gets 2 dynamic values, task_id
and project_id . We’re not using the second one yet, but we’ll
use it later.
Adda waytomarktasks asdone
Let’s now add a little “checkmark icon” to tasks. Once clicked,
the task is marked as done.
Create a “check” icon in its own Astro component, in
src/components/app/icons/IconCheck.astro :
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 69/104
clip-rule="evenodd">
</path>
</svg>
---
import IconCheck from '@components/app/icons/IconCheck.astro'
const { task } = Astro.props
---
<form
hx-put={`/app/api/project/${task.project}/task/${task.id}`}
hx-target='this'
hx-trigger='click'
hx-swap='none'
hx-vals=`{"action": "${task.completed ? 'uncheck' :
'check'}"}`>
<div
class={`${
task.completed ? 'bg-green-500' : ' bg-gray-500'
} h-8 w-8 rounded-full flex items-center justify-center
ring-2 ring-white cursor-pointer`}>
<IconCheck />
</div>
</form>
Then we create the
src/components/app/tasks/CompleteTaskButton.astro component:
This component includes the “check” icon and we wrap it into a
form. When the element is clicked, we make a PUT request to update
the task with the action “check” if the task was not completed
yet, otherwise we send “uncheck”.
We include this component in
src/components/app/tasks/TasksList.astro :
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 70/104
---
import { getTasks } from '@data/pocketbase'
import DeleteTaskButton from
'@components/app/tasks/DeleteTaskButton.astro'
import CompleteTaskButton from
'@components/app/tasks/CompleteTaskButton.astro'
const { project_id } = Astro.props
const tasks = await getTasks(project_id)
---
{
tasks.length === 0 && (
<p class='text-center text-zinc-900 dark:textwhite'>Nothing yet</p>
)
}
<ul class='space-y-6 mb-10'>
{
tasks.map(task => (
<li>
<div class='flex justify-between'>
<div class='flex justify-between space-x-4 itemscenter'>
<div>
<CompleteTaskButton task={task} />
</div>
<div>{task.text}</div>
<div class='flex-1'>{task.text}</div>
<div>
<DeleteTaskButton task={task} />
</div>
</div>
</li>
))
}
</ul>
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 71/104
---
export const partial = true
import { deleteTask } from '@data/pocketbase'
import { deleteTask, updateTask } from '@data/pocketbase'
import TasksList from '@components/app/tasks/TasksList.astro'
const { task_id = '', project_id = '' } = Astro.params
if (Astro.request.method === 'DELETE') {
await deleteTask(task_id)
return new Response(null, { status: 200 })
}
Here’s the result so far:
When clicked, the button makes a PUT HTTP request to
/app/api/project/<PROJECT_ID>/task/<TASK_ID> .
So we handle that HTTP request in
src/pages/app/api/project/[project_id]/task/[task_id].astro
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 72/104
if (Astro.request.method === 'PUT') {
const formData = await Astro.request.formData()
const action = formData.get('action') as string
if (action === 'check') {
await updateTask(task_id, {
completed: true,
completed_on: new Date().toISOString(),
})
} else if (action === 'uncheck') {
await updateTask(task_id, {
completed: false,
completed_on: '',
})
} else {
return new Response('Invalid action', { status: 400 })
}
}
---
<div id='tasks-todo' hx-swap-oob='true'>
<TasksList project_id={project_id} />
</div>
import type {
ProjectsRecord,
ProjectsResponse,
TasksRecord,
Notice how we handle the check and uncheck actions we talked about
before.
In both cases we call updateTask() , also setting the
completed_on field so we know when a task was set as done.
We don’t have this function yet, so we add this function to
src/data/pocketbase.ts :
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 73/104
TypedPocketBase
} from '@src/data/pocketbase-types'
//...
export async function updateTask(
id: string,
data: TasksRecord
) {
await pb.collection('tasks').update(id, data)
}
<div id='tasks-todo' hx-swap-oob='true'>
<TasksList project_id={project_id} />
</div>
Going back to the previous snippet, notice this part in the
returned HTML:
This is super important, and key to making our app work nicely.
This is something called “out of band swaps”.
Read more on
https://thevalleyofcode.com/htmx/5-swap
https://htmx.org/attributes/hx-swap-oob/
and come back.
Basically we tell htmx to take this item we return and swap it
into the item with id tasks-todo (hint: the real magic is when
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 74/104
you’ll find out you can swap multiple elements in a page in a
single response).
Try setting a todo as done now, you’ll see instant feedback in
your app:
Show “done” tasks inadifferentlist
One design decision we make in the app now is to put the tasks
already completed into a separate list.
I think this will make OOB swaps “click” for you
Let’s do this in 2 steps.
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 75/104
<div class='space-y-6'>
<div
First I’m going to add a new “block” in the project page, right
between “Tasks to do” and the “Danger zone”:
I’ll call it “Tasks already done”, and we drop the <TasksList />
component again.
This time the id of its container div is tasks-done :
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 76/104
class='p-10 text-white rounded-lg shadow bg-zinc-100
dark:bg-zinc-800'>
<h2
class='pb-10 text-xl font-black text-center uppercase
text-zinc-800 dark:text-white'>
Tasks to do
</h2>
<div id='tasks-todo'>
<TasksList project_id={project_id} />
</div>
<ButtonAddNewTask project_id={project_id} />
</div>
<div
class='p-10 text-white rounded-lg shadow bg-zinc-100
dark:bg-zinc-800'>
<h2
class='pb-10 text-xl font-black text-center uppercase
text-zinc-800 dark:text-white'>
Tasks already done
</h2>
<div id='tasks-done'>
<TasksList project_id={project_id} />
</div>
</div>
<div
class='p-10 text-white rounded-lg shadow bg-zinc-800'>
<h2
class='pb-0 text-xl font-black text-center uppercase
font-rounded'>
Danger zone
</h2>
<div class='w-full mx-auto text-center'>
<button
hx-delete={`/app/api/project/${project_id}`}
hx-confirm='Are you sure?'
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 77/104
class='px-3 py-2 mx-auto mt-5 mr-2 text-sm fontmedium leading-4 text-white border border-transparent
rounded-md shadow-sm bg-zinc-600 hover:bg-red-700
focus:outline-none focus:ring-2 focus:ring-offset-2
focus:ring-red-500'>
Delete project
</button>
</div>
</div>
</div>
If you try changing the “done” status now, you’ll see only the top
block actually shows changes immediately:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 78/104
<div id='tasks-todo' hx-swap-oob='true'>
<TasksList project_id={project_id} />
</div>
<div id='tasks-done' hx-swap-oob='true'>
<TasksList project_id={project_id} />
</div>
Now add this to the returned HTML from
src/pages/app/api/project/[project_id]/task/[task_id].astro :
…and everything is in sync!
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 79/104
<div id='tasks-todo' hx-swap-oob='true'>
Now we have to tell <TaskList /> to only show “to-do” or “done”
tasks depending on what we want to display.
We can do so using a done prop in
src/pages/app/api/project/[project_id]/task/[task_id].astro
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 80/104
<TasksList project_id={project_id} />
<TasksList done={false} project_id={project_id} />
</div>
<div id='tasks-done' hx-swap-oob='true'>
<TasksList project_id={project_id} />
<TasksList done={true} project_id={project_id} />
</div>
<div
class='p-10 text-white rounded-lg shadow bg-zinc-100
dark:bg-zinc-800'>
<h2
class='pb-10 text-xl font-black text-center uppercase
text-zinc-800 dark:text-white'>
Tasks to do
</h2>
<div id='tasks-todo'>
<TasksList project_id={project_id} />
<TasksList done={false} project_id={project_id} />
</div>
<ButtonAddNewTask project_id={project_id} />
</div>
<div
class='p-10 text-white rounded-lg shadow bg-zinc-100
dark:bg-zinc-800'>
<h2
class='pb-10 text-xl font-black text-center uppercase
text-zinc-800 dark:text-white'>
Tasks already done
</h2>
We do the same in src/pages/app/project/[project_id].astro :
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 81/104
<div id='tasks-done'>
<TasksList project_id={project_id} />
<TasksList done={true} project_id={project_id} />
</div>
</div>
const { project_id } = Astro.props
const { project_id, done } = Astro.props
const tasks = await getTasks(project_id)
const tasks = await getTasks({ project_id, done })
export async function getTasks(project_id: string) {
export async function getTasks({
project_id = null,
done = false,
}) {
const options = {
filter: `project = "${project_id}"`,
filter: '',
}
let filter = `completed = ${done}`
filter += ` && project = "${project_id}"`
options.filter = filter
const tasks = await pb
Now in src/components/app/tasks/TasksList.astro we get the
done prop and we pass it to getTasks :
We change how we get the parameters in getTasks() in
src/data/pocketbase.ts , and we change how we filter tasks by
project, only filtering if a project id was passed to the
function:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 82/104
.collection('tasks')
.getFullList(options)
return tasks
}
Now done tasks appear in the second list, and undone tasks appear
in the first one:
Star a task
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 83/104
if (action === 'check') {
await updateTask(task_id, {
completed: true,
completed_on: new Date().toISOString(),
})
} else if (action === 'uncheck') {
await updateTask(task_id, {
completed: false,
completed_on: '',
})
} else if (action === 'star') {
await updateTask(task_id, {
starred: true,
starred_on: new Date().toISOString(),
})
} else if (action === 'unstar') {
await updateTask(task_id, {
starred: false,
starred_on: '',
})
} else {
return new Response('Invalid action', { status: 400 })
}
---
const { active } = Astro.props
Similarly to how we made it possible to “check” a task, let’s make
it possible to “star” it, so a task with priority gets more
visibility in the list.
First we add 2 more possible actions in our PUT request handler in
src/pages/app/api/project/[project_id]/task/[task_id].astro :
Then we create a “star” icon in
src/components/app/icons/IconStar.astro
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 84/104
---
<svg
xmlns="http://www.w3.org/2000/svg"
fill={`${active ? 'rgb(234, 179, 8)' : 'none'}`}
viewBox="0 0 24 24"
stroke-width="1.5"
stroke={`${active ? 'rgb(234, 179, 8)' : 'currentColor'}`}
class="w-6 h-6 text-[rgb(234,179,8)]">
<path
stroke-linecap="round"
stroke-linejoin="round"
d="M11.48 3.499a.562.562 0 011.04 0l2.125 5.111a.563.563
0 00.475.345l5.518.442c.499.04.701.663.321.988l-4.204
3.602a.563.563 0 00-.182.557l1.285 5.385a.562.562 0
01-.84.61l-4.725-2.885a.563.563 0 00-.586 0L6.982
20.54a.562.562 0 01-.84-.61l1.285-5.386a.562.562 0
00-.182-.557l-4.204-3.602a.563.563 0
01.321-.988l5.518-.442a.563.563 0 00.475-.345L11.48 3.5z">
</path>
</svg>
---
import IconStar from '@components/app/icons/IconStar.astro'
const { task } = Astro.props
---
<div class='flex-none cursor-pointer'>
<form
hx-put=
{`/app/api/project/${task.project}/task/${task.id}`}
hx-target='this'
hx-trigger='click'
hx-swap='none'>
We use it in a new component we add in
src/components/app/tasks/StarTaskButton.astro :
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 85/104
<input
type='hidden'
name='action'
value={task.starred ? 'unstar' : 'star'}
/>
<div>
<IconStar active={task.starred} />
</div>
</form>
</div>
---
import { getTasks } from '@data/pocketbase'
import DeleteTaskButton from
'@components/app/tasks/DeleteTaskButton.astro'
import CompleteTaskButton from
'@components/app/tasks/CompleteTaskButton.astro'
import StarTaskButton from
'@components/app/tasks/StarTaskButton.astro'
const { project_id, done } = Astro.props
const tasks = await getTasks({ project_id, done })
---
{
tasks.length === 0 && (
<p class='text-center text-zinc-900 dark:textwhite'>Nothing yet</p>
)
}
<ul class='space-y-6'>
{
tasks.map(task => (
<li>
and we include this in src/components/app/tasks/TasksList.astro :
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 86/104
<div class='flex justify-between space-x-4 itemscenter'>
<div>
<CompleteTaskButton task={task} />
</div>
<div>
<StarTaskButton task={task} />
</div>
<div class='flex-1'>{task.text}</div>
<div>
<DeleteTaskButton task={task} />
</div>
</div>
</li>
))
}
</ul>
This should “just work”, you can star or un-star tasks in the
list:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 87/104
export async function getStarredTasks() {
const options = {
sort: '-starred_on',
filter: 'starred = true && completed = false'
}
let tasks = await pb
.collection('tasks')
.getFullList(options)
return tasks
}
---
import { getTasks } from '@data/pocketbase'
import { getTasks, getStarredTasks } from '@data/pocketbase'
Show starredtasks inthedashboard
One cool thing we can do now is gather all starred tasks, from all
projects, and display them in the dashboard, before the projects
list.
We can add a getStarredTasks() function to
src/data/pocketbase.ts to retrieve starred tasks, ordered by
last starred date:
Note that we could have reused getTasks but I think it’s worth
having a dedicated function.
Now in src/components/app/tasks/TasksList.astro we can accept a
starred prop, and if that is set, we list starred tasks from
across all projects:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 88/104
//...
const { project_id, done } = Astro.props
const { project_id, done, starred } = Astro.props
const tasks = await getTasks({ project_id, done })
let tasks = null
if (starred) {
tasks = await getStarredTasks()
} else {
tasks = await getTasks({ project_id, done })
}
---
{
tasks.length === 0 && (
tasks.length === 0 && !starred && (
<p class='text-center text-zinc-900 dark:textwhite'>Nothing yet</p>
)
}
import TasksList from '@components/app/tasks/TasksList.astro'
We also print “Nothing yet” only if we’re listing tasks in a
project, not starred tasks:
Now in src/pages/app/dashboard.astro we can add this at the top:
and then we can add this list in the template:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 89/104
<LayoutApp title='Dashboard'>
<div class='mx-auto text-white max-w-7xl space-y-6'>
<div
class='rounded-lg bg-zinc-900 px-5 py-4 sm:py-2.5 textxl sm:text-2xl md:text-3xl text-white uppercase text-center
font-extrabold font-rounded'>
<div class='sm:hidden'>
<HamburgerMenuButton />
</div>
Projects
</div>
<div id='starred-tasks-list'>
<TasksList starred={true} />
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
You should see (undone) starred tasks in the dashboard!
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 90/104
Now any action we performed on tasks is possible also in this list
(you can mark a task as done, or un-star it), but we don’t get
immediate feedback on those actions
Add this to
src/pages/app/api/project/[project_id]/task/[task_id].astro :
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 91/104
<div id='tasks-todo' hx-swap-oob='true'>
<TasksList done={false} project_id={project_id} />
</div>
<div id='tasks-done' hx-swap-oob='true'>
<TasksList done={true} project_id={project_id} />
</div>
<div id='starred-tasks-list' hx-swap-oob='true'>
<TasksList starred={true} />
</div>
<ul class='space-y-6'>
{
tasks.map(task => (
<li>
<div class='flex justify-between space-x-4 itemscenter'>
<div>
<CompleteTaskButton task={task} />
</div>
<div>
<StarTaskButton task={task} />
</div>
<div class='flex-1'>{task.text}</div>
<div>
<DeleteTaskButton task={task} />
</div>
{starred && (
so any action now performs an out-of-band swap for #starredtasks-list too.
I think we can improve starred tasks visualization by also showing
the project they belong to, something we didn’t need in the
projects view.
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 92/104
<div>
<a href={`/app/project/${task.project}`}>
<span class='border mt-0 py-0.5 px-2 selfstart rounded-md bg-zinc-800 text-sm font-bold hidden
sm:block'>
{task.expand?.project?.name}
</span>
</a>
</div>
)}
</div>
</li>
))
}
</ul>
export async function getStarredTasks() {
const options = {
sort: '-starred_on',
filter: `starred = true && completed = false`,
expand: 'project',
}
let tasks = await pb
.collection('tasks')
.getFullList(options)
return tasks
}
Notice I used task.expand to get access to the name property
of the project this task is linked to.
To get this data, we must ask for it in src/data/pocketbase.ts :
However you’ll quickly notice a TypeScript error:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 93/104
import type {
TypedPocketBase,
ProjectsResponse,
ProjectsRecord,
TasksRecord,
TasksResponse,
} from '@src/data/pocketbase-types'
type TexpandProject = {
project?: ProjectsResponse
}
TS doesn’t automatically pick up this relation.
We have to do a little bit of TS work here, I think it’s the only
case in the app we have to mess a bit with types.
First we import TasksResponse :
and we define this type, basically we tell “we expand with a
project property that’s of type ProjectsResponse ”:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 94/104
export async function getStarredTasks() {
export async function getStarredTasks(): Promise<
TasksResponse<TexpandProject>[]
> {
const options = {
sort: '-starred_on',
filter: `starred = true && completed = false`,
expand: 'project',
}
let tasks: TasksResponse<TexpandProject>[] = []
tasks = await pb.collection('tasks').getFullList(options)
return tasks
}
let tasks = null
if (starred) {
tasks = await getStarredTasks()
} else {
tasks = await getTasks({ project_id, done })
}
Then we use this type for both the tasks variable, and the
return type of getStarredTasks() :
Now things should be working, but the TS error is still there
since in TasksList tasks can be returned from both
getStarredTasks and getTasks , we should return the same type
from both.
We’ll later eventually need the project info from tasks returned
in getTasks too, so we use the same type in that function as
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 95/104
export async function getTasks({
project_id = null,
done = false,
}): Promise<TasksResponse<TexpandProject>[]> {
const options = {
filter: '',
expand: 'project',
}
let filter = `completed = ${done}`
filter += ` && project = "${project_id}"`
options.filter = filter
let tasks: TasksResponse<TexpandProject>[] = []
const tasks = await pb
tasks = await pb
.collection('tasks').getFullList(options)
return tasks
}
well:
Everything should be working fine now.
The only thing is, here is a bit crowded:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 96/104
<div>
<DeleteTaskButton task={task} />
</div>
{starred && (
{starred ? (
<div>
<a href={`/app/project/${task.project}`}>
<span class='border mt-0 py-0.5 px-2 self-start
rounded-md bg-zinc-800 font-bold text-sm hidden sm:block'>
{task.expand?.project?.name}
</span>
</a>
</div>
) : (
Let’s remove the delete button in this view:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 97/104
<div>
<DeleteTaskButton task={task} />
</div>
)}
Looks better:
Editthetasktext
The final thing I want to do is allowing to edit the task text.
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 98/104
if (action === 'check') {
await updateTask(task_id, {
completed: true,
completed_on: new Date().toISOString(),
})
} else if (action === 'uncheck') {
await updateTask(task_id, {
completed: false,
completed_on: '',
})
} else if (action === 'star') {
await updateTask(task_id, {
starred: true,
starred_on: new Date().toISOString(),
})
} else if (action === 'unstar') {
await updateTask(task_id, {
starred: false,
starred_on: '',
})
} else if (action === 'edit-text') {
await updateTask(task_id, {
text: formData.get('task-text') as string,
})
} else {
return new Response('Invalid action', { status: 400 })
}
<div class='flex-1'>{task.text}</div>
We add a edit-text action to
src/pages/app/api/project/[project_id]/task/[task_id].astro :
Then in src/components/app/tasks/TasksList.astro
Where we now have this:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 99/104
---
const { task } = Astro.props
---
<div class='flex-1'>
{task.text}
</div>
---
import { getTasks, getStarredTasks } from '@data/pocketbase'
import DeleteTaskButton from
'@components/app/tasks/DeleteTaskButton.astro'
import CompleteTaskButton from
'@components/app/tasks/CompleteTaskButton.astro'
import StarTaskButton from
'@components/app/tasks/StarTaskButton.astro'
import TaskText from '@components/app/tasks/TaskText.astro'
const { project_id, done, starred } = Astro.props
let tasks = null
if (starred) {
tasks = await getStarredTasks()
} else {
tasks = await getTasks({ project_id, done })
}
---
{
tasks.length === 0 && !starred && (
We can extract this to its own component in a new file called
src/components/app/tasks/TaskText.astro :
Here’s the new src/components/app/tasks/TasksList.astro :
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 100/104
<p class='text-center text-zinc-900 dark:textwhite'>Nothing yet</p>
)
}
<ul class='space-y-6'>
{
tasks.map(task => (
<li>
<div class='flex items-center justify-between spacex-4'>
<div>
<CompleteTaskButton task={task} />
</div>
<div>
<StarTaskButton task={task} />
</div>
<div class='flex-1'>{task.text}</div>
<TaskText task={task} />
{starred ? (
<div>
<a href={`/app/project/${task.project}`}>
<span class='border mt-0 py-0.5 px-2 selfstart rounded-md bg-zinc-800 text-sm font-bold hidden
sm:block'>
{task.expand?.project?.name}
</span>
</a>
</div>
) : (
<div>
<DeleteTaskButton task={task} />
</div>
)}
</div>
</li>
))
}
</ul>
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 101/104
---
const { task } = Astro.props
---
<div class='flex-1' x-data='{ editable: false }'>
<div
x-show='!editable'
class='text-zinc-800 dark:text-zinc-200'
@dblclick=`
editable = true
//put the sibling input on focus
$nextTick(() => {
const inputfield =
$el.nextElementSibling.querySelector('input#task-text')
inputfield.focus()
inputfield.select()
})
`>
{task.text}
</div>
<form
x-show='editable'
x-cloak
hx-put=`/app/api/project/${task.project}/task/${task.id}`
hx-trigger='change'
hx-target='this'
hx-swap='none'
We can now work on that component to implement editing the task
name, using a mix of Alpine and htmx.
In src/components/app/tasks/TaskText.astro replace the content
with this code:
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 102/104
class='w-full'
hx-vals=`{"action": "edit-text"}`>
<input
name='task-text'
id='task-text'
class='w-full px-0 -mt-2 bg-transparent outline-none
text-zinc-800 dark:text-zinc-200 border-zinc-800 dark:borderzinc-200'
value={task.text}
@keydown.enter.prevent=`editable = false`
@keydown.escape.prevent=`editable = false`
@blur=`editable = false`
@click.outside='editable = false'
/>
</form>
</div>
What is happening here?
We use the @dblclick Alpine.js attribute to run some code when
the element is double-clicked. In this code we set the editable
property (defined on the parent div using x-data ) to true , and
we put the form element on focus using some Web DOM APIs
( querySelector() , focus() and select() ).
We won’t use those APIs anywhere else in the project, but here
they are quite useful to interact with the elements displayed on
the page.
We show a <div> if the element is not editable, and a form (with
a single text input box) if the element is editable.
This form sends a PUT request to our “edit task” route when its
content is changed (using the hx-trigger attribute).
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 103/104
Pressing “enter” or “esc” will set editable to false again,
and we detect this using Alpine’s @keydown.enter event. Same
with clicking outside of the form item using @click.outside and
when focus changes (using @blur ).
It’s a mix of htmx and Alpine.js “magic” combined to make things
work.
In practice what happens is that you double click a task, and it’s
editable.
Stop editing and focus on something else, or press enter, and the
new task text is saved.
Thanks to how we built the app, this is possible both in the
individual project page, but also in the starred tasks list in the
dashboard.
Wrappingup
In this module we did a ton of improvements to our app and now
it’s starting to feel like an app worth using, something is
moving, and we’re just getting started actually.
Everything in our app is now “global”, there are no users, no
login, if we deployed the app now on the Internet, people would
just see a total mess because everyone could add projects and
tasks.
In the next module we’ll implement login and users, so every user
will only see their own private data.
4/19/24, 4:39 AM Module 4
https://2024.bootcamp.dev/modules/module-4/ 104/104
NOTE: find the full code of this module on
https://github.com/flaviocopes/bootcamp-2024/tree/mod4
This was the content of this module:
1: Introduction to the module
2: Add a sidebar
3: List projects in the sidebar
4: Add hamburger menu to show projects list on mobile
5: Add x-cloak to prevent flicker
6: Moving styles to app.css
7: Use hx-boost to smooth navigation
8: Sort projects by status
9: Fix the TS errors
10: Use the logo font for the pages title
11: Delete a project
12: Allow to edit the project status
13: Let people edit the project’s name.
14: Delete a task
15: Add a way to mark tasks as done
16: Show “done” tasks in a different list
17: Star a task
18: Show starred tasks in the dashboard
19: Edit the task text
20: Wrapping up
[← back to all the Bootcamp modules]
