---
title: Module 1
date: 4/1/2024
myData: Introduction to the module, The app requirements, How we’re going to store the data, Data modeling after the requisites, PocketBase installation options, Explore PocketBase,
---

# Hi there! Welcome to class!!!

This Markdown file creates a page at [localhost:4321/blog/my](#)

It probably isn't styled much, but Markdown does support:

- **bold** and _italics._
- lists
- [Modules](/blog)
- and more!

## Content

1. [Introduction to the module](#introduction-to-the-module)
2. [The app requirements](#the-app-requirements)
3. [How we’re going to store the data](#how-we-are-going-to-store-the-data)
4. [Data modeling after the requisites](#data-modeling)
5. [PocketBase installation options](#pocketbase-installation)
6. [Explore PocketBase](#explore-pocketbase)
7. [The collections API Rules](#the-collection-api-rules)
8. [Users collection options](#users-collection-options)
9. [The PocketBase API Preview](#the-pocketbase-api-preview)
10. [PocketBase Logs](#pocketbase-logs)
11. [PocketBase System settings](#pocketbase-sytem-settings)
12. [Create the projects collection on PocketBase](#create-the-projects-collection-on-pocketbase)
13. [Create the tasks collection on PocketBase](#create-the-tasks-collection-on-pocketbase)
14. [Editing the API Rules](#editing-the-api-rules)
15. [Wrapping up the module](#wrapping-the-module)
16. [top](#)

[← back to all modules](/blog)

## Goals

[&rarr; top](#)

Define the problem, understand the problem, define both the application and the architecture. Install PocketBase locally. Start some initial data modeling. Create collections.

## Introduction to the module

[&rarr; top](#)

The goal is to build from scratch a complex application that will allow you to explore techniques and challenges solving problems that may include:

1. storing data
1. gathering data with the correct permissions
1. authenticating users
1. handling payments and subscriptions
1. caching
1. security

among others.

In this module we are going to focus on what our application requirements are. Also I am going to explain why are we are to pick the tech stack we will use in this class.

The project is based on the latest Flavio Copes bootcamp so some of the materials are coming from his github account, as well as from the bootcamp itself.

Our hope is that by building the application you will allow you to learn techniques and patterns that you will apply to any kind of web application in the future.

We will build a SaaS app: a project management SaaS app for individuals and teams. Flavio Copes called it "Secretplan".
I am borrowing heavily on his materials and giving you a small taste of what a bootcamp entails.

"Software as a Service" is an app we distribute on the Web, and people instead of downloading it will use it from the website. Sometimes you can download the app into different devices, but it is still a SaaS app.

The skills you learn will allow you to create your own products and run your own microbusinnes on the Internet as a developer, working from anywhere in the world.

## The app requirements

[&rarr; top](#)

There some user stories you will have to solve in the app:

1. Loggin into the app with email and password (no dependency on 3d party providers)
1. Once the user is logged in, he/she can manage multiple personal projects
1. Once a project is created, people can add a 'task', for example project 'my website' has a task called 'create personal page'
1. The app allows to mark a task as done and remove it from the list of tasks to be done
1. A task can be starred to mark it as important and visually separate it from all the other tasks
1. A project has status, so it starts as 'not started', and change the status as the project move along until it is 'done'.
1. The app allows to attach pictures to a task.

For everything the app will have a responsive design so it looks nice no matter what device is being used to run it.

## How we are going to store the data

[&rarr; top](#)

Data will be stored in a database. The choice is wide (sql-type and non-sql type databases). Historically we have used mongo database which is a nonsql type database. This year I will offer a sort of mixture between both types: it is called Pocketbase.

Maybe you've heard of Firebase or Supabase. They are tools that provide database services. In addition, they provide some convenient features: authentication, image uploads, authorization rules, so as a developer you do not have to worry about when writing your code.

Pocketbase is similar in functionality but it offers a great advantage: it is free and self-hosted. No need to pay a fee for the service on the cloud or to download and configure in your laptop when you want to self host it (which probably is impossible).

Pocketbase is very simple to manage: it is a single binary file written in Go programming language, and one of the benefits of Go is that programs are just that, single binaries.

We will interact with it using JavaScript (more preciselly TypeScript, to get the convenience of improved error checking and auto-completion in VS Code).

All data internally is stored in an SQLite relational database, entirely stored in a pb_data folder, so it is super easy to backup or restore data. Also, there is no 'lock-in' because you can move your data anywhere else if you want to.

This setup can scale up very well, all you have to do is purchase a more powerful (cloud based) server to run it.

Of course, when your user base incresase from few thousands to possibly millions you can gradually move away from it, and into other database services. By then, you already have a successful business to run in your hands.

Most apps you'll build will never reach that stage. Most apps get zero users.

With Pocketbase you could build 10 different apps in very little time and see which ones to trash and which ones to develop further.

## Data modeling

[&rarr; top](#)

Earlier in this document we talked about projects, tasks, users.

So please the following user stories that your code will tackle and resolve:

1. A user can create one (or many) projects. He/she is the project owner. No one else can see that project, or add tasks to it.
1. A project has multiple tasks assigned to it. It could be zero tasks, or 10000
1. A task is assigned to a single project. The user cannot have a task that belongs to multiple projects.
1. As admin you will track all the activites across projects

## PocketBase installation

[&rarr; top](#)

The installation binaries are in your laptop in the 'Public' folder.
The file is 'pocketbase_0.22.8_windows_amd64.zip'. Extract the file in /c/Users/PublicPrograms/ folder. cd into the folder, right-click in your touchpad, open terminal (any terminal, cmd or gitbash or powershell). Start pocketbase by typing in the command line

```

./pocketbase serve (gitbash)

or

.\pocketbase.exe serve (windows command line or powershell).

```

As for your app, and in order to keep things organized, you will create a folder labeled 'QUARTER-3' inside your Documents folder. Everything related to our class will be in that folder. Or, if you have your class folder in the Desktop, you can keep using the Desktop for our class materials. It is up to you, as long as you can identify and easily find our class materials including submissions, labs, reading materials, etc.

Once the serve starts, go to chrome browser, type either URL

```

'http://localhost:8090/_/'

or

'http://127.0.0.1:8090/_/'

```

to access the Admin UI.

The first time you will see the setup screen with the text

```

'Create your first admin account in order to continue'.

```

For the email field use your

```

lastName first initial @ voced dot ed.

```

Enter an easy to remember password. Choose a not very complex password since we are not going to store anything important, just we want to practice. If you forget your admin password there are ways to recover it, so do not worry. Once you create your admin account, click the 'Create and login' button.

If you are a night owl, PocketBase does not offer a dark mode feature, but you can use a browser extension to display it dark, like 'Dark Reader'. Please remind me to pass it to you in class.

## Explore PocketBase

[&rarr; top](#)

PocketBase is tiny, yet powerful.

You have 3 main sections on the PocketBase dashboard: Collections, Logs, and Settings.

'Collections' is what you see first after setting up admin account.

Data is managed through 'collections'.

PocketBase already created a 'users' collection.

You can see a button to add new collection and a button to add new record to the collection.

If you click 'New Record' you will see a form showing up to add the new record data fields: id, Username, Email, Password, Verified, name, avatar, and the 'cancel' and 'Create' buttons.

The default user collection is set up for basic user data. We can add a username, email, password, a verified field as boolean, a name, and an avatar, which is an image.

Later we will be adding users. For now just explore the GUI.

Click the 'gear' icon.

It allows you to edit the collection. In this case it shows the user collection. The user collection is special. You have some system fields like id, created, email, etc. At the top you have the field name and avatar.

You can add more if you want. You can choose from various formats and types: Plain text, Email, File, Rich Editor, Url, Relation, Number, Datetime, JSON, Bool, and Select.

### The collection API Rules

[&rarr; top](#)

In the API Rules panel you can set permissions to perform **CRUD** operations: Create / Read / Update / Delete and List/Search operation.

This panel is important in the app security. You can enforce security on the data by correctly setting those API rules.

The default rule is:

```

id = @request.auth.id

```

which means 'the id field of the collection must match the id of the currently authenticated user'

Simply stated: users can only access their own user data.

To make data public for all, you can clear a rule content by deleting it. You can see the text 'View rule Leave empty to grant everyone access...'

We will tweak the rules later.

### Users collection options

[&rarr; top](#)

The last tab on the panel is "Options" tab. PocketBase allows 3 different authentication methods: username/password, email/password, and OAuth2 (login with Google, etc).

Disable OAuth2, and username/password, we we will use email/password based authentication in the class.

Also, enable 'Always require email'. Press 'Save changes' button to apply the changes.

### The PocketBase API Preview

[&rarr; top](#)

Now try clicking the 'API Preview' button.

PocketBase has built-in documentation about how to interface with it using JavaScript. Take a look around, explore the documentation, review the offline PocketBase documentation site at http://localhost:22022/pocketbase URL in your browser.

The offine web site did not downloaded completely. After you start visiting a link, the left side menu links may not work. Just go back and try again, or visit the original URL in the previous paragraph and try the link again.

### PocketBase Logs

[&rarr; top](#)

You can visualize all connection logs. Clicking each request data will give you more details. This is very useful when debugging your app, or to figure out what runs too slow. You will be able to filter requests by log level and API route.

### PocketBase Sytem settings

[&rarr; top](#)

In the application panel, you can set the application name. Let's call it **SPRING24APP**

In 'Mail settings' you can configure the email sender name/email, and the emails sent when the users register.

In a real app, you'll also want to configure a SMTP mail server to actually send emails.

An SMTP server definition:

<!-- ![](/smtp-server.png) -->
<img src="/image/smtp-server.png" alt="smtp server" width=50% style="border:10px solid orange">
<!-- <img src="../smtp-server.png" alt="smtp server" width=50%> -->

If we have time I will set up a SMTP server in class, as well as in your laptops, so you could see all the emails that your app sends, only if we have time.

In 'File storage' you can set AWS S3 compatible storage for file uploads. This is useful if you plan to have a lot of file uploads on your app.

In 'Backups' you can create backup, and restore previous data backups.

In 'Export collections' you can export the collections as JSON and import them in 'Import collections in another pocketBase installation, to move aroung your collections setup (but not the data).

In 'Auth providers' there is OAuth2 auth setup that we won't use.

In 'Token options' you can tweak the application token durations.

In 'Admins' you can add other admin users to the PocketBase instance.

## Create the projects collection on PocketBase

[&rarr; top](#)

Based on the data we defined earlier, we're now going to define these collections:

1. projects
1. tasks

Click the 'New collection' button.

Enter 'projects' as the name of the collection.
PocketBase tells you every collection by default has an id field that will be a uniquely generated string, created and updated fields that will contain the dates each record was created, or updated (automatically kept up to date by the PocketBase).

Click 'New field'. Choose a field type. A project will have a name, a string, so we choose 'Plain text'. You will see a 'T' appearing in the field. Enter its name.

The project will have a status. A project will be either not started, started, in progress, almost finished, done, ongoing, on hold, or archived. We could use a text field since the it is a limited number of options, but PockeBase has a 'Select' field.

The select type allow you to write the options separated by a comma.

Then we need to store information about who created the project. We need to select the 'Relation' type that link the project name with an user. Type in the field created_by. The 'Single' option next to both the Select and Relation field types means a project can only have one status (not multiple), and a project can only have a user who created it.

Click the little gear icon &#9881; at the far right on the field.

<!-- ![](/created_by_img.png) -->
<img src="/image/created_by_img.png" alt="/created by" width=50%>

The 'Cascade delete' option is very interesting. If an user is deleted, by selecting cascade delete allows to automatically delete the projects associated to that user. It is useful, because all the work happens under the hood just by enabling the checkbox. Set it to 'true'. Finally, click the 'Create' button.

The new collection should now be visible.

## Create the tasks collection on PocketBase

[&rarr; top](#)

Similarly, let's create a new collection: tasks.

A task is associated with a project, so we add a project 'Relation' field that is connected to the 'projects' collection. Click on the gear icon to the right to set it to 'Cascade delete' to true to delete tasks when a project is deleted (and in turn when an user is deleted).

Add a 'Plain text' field that will hold the task text. Text fields have some options too, but we're not going to set any yet.

A task can be marked as completed, so we add a completed field of type 'Bool', and a completed_on field of type 'DateTime'.

A task can be starred, so we add starred ('Bool' type) and starred_on ('DateTime').

If you make a mistake you can always remove the field by clicking the gear icon then the little ... icon, then click remove.

We'll allow people to associate an image with a task. We'll use an image field of type 'File' to do that, setting it to enable multiple files, for a maximum of 10, we'll also just allow the most common image mime types: jpeg, png, gif, webp

There is also a preset, you can see by clicking 'Choose presets'.

Now enable loading multiple images, and set how many (select 10)

Now we can set various thumbnail sizes, so we don't make users download full images when not needed. We'll add 0x800 and 0x200 as our thumb sizes. the former resized to a height of 800 pixels, preserving the aspect ratio. The latter to 200 pixels for the thumbnails.

We have also a maximum file size (5 MB).

Finally, select a new field, type created_by, associate the task to the person who created it, like we did for the projects collection. Click 'Relation' set 'Cascade delete' to true.

Click the 'Create' button.

The collection was created.

## Editing the API rules

[&rarr; top](#)

One extremely important functionality PocketBase provides ia we can set authorization rules upon each operation we can perform on the collection data: list/search, read, update, delete, and create (**CRUD** operations).

If you open the users collection and click the gear to edit the settings, in the API rules tab you'll see the default rules for the table: only the currently authenticated user can view, list/search, update or delete users. Anyone can create them (since when someone creates an account, they're not logged in yet). You'll see

```

id = @request.auth.id

```

or

```

Leave empty to grant everyone access...

```

Now switch to projects collection: by default, no rule is set:

which means **nobody can do anything**

If you hover over one of the rules you'll see a hint:
`Unlock and set custom rule`
You can click the item and now if you save the rules, everyone can list the projects.

For now, let's remove all API rules by clicking each item, and set it to 'Leave empty to grant everyone access...'

Do this for both the projects and tasks collections.

We'll implement security rules and add authentication later.

## Wrapping the module

[&rarr; top](#)

- We defined our app functionality
- set data model
- set up collections
- set up API rules

[&rarr; top](#)
