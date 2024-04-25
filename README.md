# Astro Starter Kit: Basics

```sh
npm create astro@latest -- --template basics
```

[![Open in StackBlitz](https://developer.stackblitz.com/img/open_in_stackblitz.svg)](https://stackblitz.com/github/withastro/astro/tree/latest/examples/basics)
[![Open with CodeSandbox](https://assets.codesandbox.io/github/button-edit-lime.svg)](https://codesandbox.io/p/sandbox/github/withastro/astro/tree/latest/examples/basics)
[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/withastro/astro?devcontainer_path=.devcontainer/basics/devcontainer.json)

> 🧑‍🚀 **Seasoned astronaut?** Delete this file. Have fun!

![just-the-basics](https://github.com/withastro/astro/assets/2244813/a0a5533c-a856-4198-8470-2d67b1d7c554)

## 🚀 Project Structure

Inside of your Astro project, you'll see the following folders and files:

```text
/
├── public/
│   └── favicon.svg
├── src/
│   ├── components/
│   │   └── Card.astro
│   ├── layouts/
│   │   └── Layout.astro
│   └── pages/
│       └── index.astro
└── package.json
```

Astro looks for `.astro` or `.md` files in the `src/pages/` directory. Each page is exposed as a route based on its file name.

There's nothing special about `src/components/`, but that's where we like to put any Astro/React/Vue/Svelte/Preact components.

Any static assets, like images, can be placed in the `public/` directory.

## 🧞 Commands

All commands are run from the root of the project, from a terminal:

| Command                   | Action                                           |
| :------------------------ | :----------------------------------------------- |
| `npm install`             | Installs dependencies                            |
| `npm run dev`             | Starts local dev server at `localhost:4321`      |
| `npm run build`           | Build your production site to `./dist/`          |
| `npm run preview`         | Preview your build locally, before deploying     |
| `npm run astro ...`       | Run CLI commands like `astro add`, `astro check` |
| `npm run astro -- --help` | Get help using the Astro CLI                     |

## 👀 Want to learn more?

Feel free to check [our documentation](https://docs.astro.build) or jump into our [Discord server](https://astro.build/chat).

## LOG

### 4.21.2024
```
npm 
npm install
npm WARN EBADENGINE Unsupported engine {
npm WARN EBADENGINE   package: '@astrojs/prism@3.1.0',
npm WARN EBADENGINE   required: { node: '^18.17.1 || ^20.3.0 || >=21.0.0' },
npm WARN EBADENGINE   current: { node: 'v18.16.0', npm: '9.5.1' }
npm WARN EBADENGINE }
npm WARN EBADENGINE Unsupported engine {
npm WARN EBADENGINE   package: '@astrojs/telemetry@3.1.0',
npm WARN EBADENGINE   required: { node: '^18.17.1 || ^20.3.0 || >=21.0.0' },
npm WARN EBADENGINE   current: { node: 'v18.16.0', npm: '9.5.1' }
npm WARN EBADENGINE }
npm WARN EBADENGINE Unsupported engine {
npm WARN EBADENGINE   package: 'astro@4.6.3',
npm WARN EBADENGINE   required: {
npm WARN EBADENGINE     node: '^18.17.1 || ^20.3.0 || >=21.0.0',
npm WARN EBADENGINE     npm: '>=9.6.5',
npm WARN EBADENGINE     pnpm: '>=7.1.0'
npm WARN EBADENGINE   },
npm WARN EBADENGINE   current: { node: 'v18.16.0', npm: '9.5.1' }
npm WARN EBADENGINE }

added 499 packages, and audited 500 packages in 7s

187 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities

```

# 2024 week 4.17

## Folder structure


```text
/
├── dist/
├── public/
│   └── favicon.svg
├── src/
│   ├── env.d.ts
│   ├── components/
│   │   └── Card.astro
│   ├── layouts/
│   │   └── Layout.astro
│   │   └── LayoutSite.astro
│   └── pages/
│       └── index.astro    EDITED to add links to my, my2, my3, offine sites
│       └── index1.astro   import LayoutSite
│       └── index3.astro    import LayoutSite
│       └── my.md
│       └── my2.md         EDITED: pics/videos source as ./ instead of /
│       └── my3.md
├── astro.config.mjs
├── .gitignore
├── package.json
├── package-lock.json
├── README.md
├── tailwin.config.mjs
├── tsconfig.json
```