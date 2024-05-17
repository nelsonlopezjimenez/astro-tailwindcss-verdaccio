---
title: Module 5
date: 5/10/2024
---

## Content

1. [content](#content)
1. [introduction](#introduction)
2. [Add signup page]
3. [Implement logout]
4. [Redirect /app to /app/dashboard]
5. [Login protect all routes and APIs]
6. [List user-specific data]
7. [New data will be associated with the current user]
8. [Forgot password]
9. [Email validation]
1. [Adding a “captcha” to auth forms with Cloudflare Turnstile]

## Introduction

In module 5 we'll introduce authentication to our app. We'll protect all routes that require auth, and we'll start creating user-specific data. All projects, tasks, etc, will be associated with a user. We'll also add forms to sign up and sign in, and reset the password. We'll let people logout too. I'll explain how to add form protection against abuse using Cloudflare Turnstile, which is available exclusively as online service (access to the cloud)

You will find the full code of this module as spring24app-module5.zip. The name of the file includes 'bootcamp' and the packages versions for dependencies may vary with yours. If a 'npm install' command does not work, delete package.json as well as package-lock.json files and use the same node_modules folder you have been running the app.

## Add signup page

We start by adding a signup page where people can enter their email, their password (twice, for confirmation) and they’ll be able to submit the form to create the account.

Create the file **src/pages/signup.astro,** and inside this file paste this code:



```

---
import LayoutSite from '@layouts/LayoutSite.astro'

let error = ''
---

<LayoutSite title='SPRING24APP'>
  <div class='w-full max-w-md mx-auto'>
    <a href='/'>
      <img
        src='/logo.svg'
        alt='Logo'
        class='h-16 mx-auto my-20 invert dark:invert-0'
      />
    </a>
  </div>

  <div
    class='mx-auto mt-10 text-white isolate gap-y-8 sm:mt-10 sm:mx-0'>
    <div
      class='flex flex-col justify-between max-w-md p-8 mx-auto bg-black border-4 rounded-3xl ring-1 ring-gray-200 xl:p-10 sm:mt-8'>
      <form method='post'>
        <p class='flex items-center justify-between mb-4'>
          <label for='email'>Email:</label>
          <input
            required
            type='email'
            name='email'
            id='email'
            class='w-2/3 p-1 text-black border'
          />
        </p>
        <p class='flex justify-between mb-4'>
          <label for='password'>Password:</label>
          <input
            required
            type='password'
            id='password'
            name='password'
            pattern='(?=.*\\d)(?=.*[a-z])(?=.*[A-Z]).{8,}'
            title='Must contain at least one number and one uppercase and lowercase letter, and at least 8 or more characters'
            class='w-2/3 p-1 text-black border'
          />
        </p>
        <p class='flex justify-between mb-4'>
          <label for='password_confirm' class='w-1/3'
            >Confirm password:</label
          >
          <input
            required
            type='password'
            id='password_confirm'
            name='password_confirm'
            pattern='(?=.*\\d)(?=.*[a-z])(?=.*[A-Z]).{8,}'
            class='w-2/3 p-1 text-black border self-baseline'
          />
        </p>
        <input
          type='submit'
          class='block w-full px-3 py-2 mt-8 text-sm font-semibold leading-6 text-center text-white rounded-md focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-blue-600 ring-1 ring-inset ring-blue-200 hover:ring-blue-300 hover:bg-blue-600'
          value='Signup'
        />
      </form>

      <p class='mt-5 text-red-500'>
        {error}
      </p>

      <p class='mt-5 text-white'>
        Already have an account? <a
          href='/login'
          class='underline'>Login</a
        >
      </p>
    </div>
  </div>
</LayoutSite>

```     

