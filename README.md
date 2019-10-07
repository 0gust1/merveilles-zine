# Merveilles-zine <!-- omit in toc -->

- [Getting started](#getting-started)
- [Adding content](#adding-content)
  - [src/routes, `src` folder](#srcroutes-src-folder)
    - [Markdown files](#markdown-files)
    - [Svelte components](#svelte-components)
    - [Server routes](#server-routes)
    - [Files <=> URLs relationship](#files--urls-relationship)
- [Website structure/organization (TODO)](#website-structureorganization-todo)
- [Design and styling (TODO)](#design-and-styling-todo)
- [PDF generation (TODO)](#pdf-generation-todo)
- [Publishing](#publishing)
- [Go further :](#go-further)

This is a quick proof of concept for a static website for the [merveilles zine intiative](https://merveilles.town/@Merristasis/102916099861136375)

The website engine is [Sapper](https://github.com/sveltejs/sapper). It offers a simplified dev experience, but generating a offline friendly performant website.



## Getting started

* Clone this repo on your machine
* install the dependencies, `npm i`
* Launch the local dev, `npm run dev`

## Adding content

The [src](src) directory contains the entry points for your app — `client.js`, `server.js` and (optionally) a `service-worker.js` — along with a `template.html` file and a `routes` directory.

### src/routes, `src` folder

This is the heart of the website. There are two kinds of routes — *pages*, and *server routes*.

*Pages* are Svelte components written in `.svelte` files **or** Markdown files (with a secret ingredient added, see below). 

When a user first visits the application, they will be served a server-rendered version of the route in question, plus some JavaScript that 'hydrates' the page and initialises a client-side router. From that point forward, navigating to other pages is handled entirely on the client for a fast, app-like feel. (Sapper will preload and cache the code for these subsequent pages, so that navigation is instantaneous.)

#### Markdown files

You can use plain markdown files. But **there is a secret**, you can also do lot more, as these files are MDSveX (the Svelte equivalent of MDX).

* [demo of MDSvex](https://mdsvex.pngwn.io/)
* [Readme + repo (feature list and doc)](https://github.com/pngwn/MDsveX)

#### Svelte components

Simple Svelte components are really easy to write. Basically, the simplest component is just a piece of HTML. But you can also do complex apps/things with it. It also really shines for aanimating stuff and generate dynamic SVG. Take a look at the examples of the offical documentation.

* [Svelte website](https://svelte.dev/)

#### Server routes

**Server routes** (which normally won't be used for the zine) are modules written in `.js` files, that export functions corresponding to HTTP methods. Each function receives Express `request` and `response` objects as arguments, plus a `next` function. This is useful for creating a JSON API, for example.

#### Files <=> URLs relationship

There are three simple rules for naming the files that define your routes:

* A file called `src/routes/about.svelte` or `src/routes/about.md` corresponds to the `/about` route. A file called `src/routes/blog/[slug].svelte` or `src/routes/blog/[slug].md` corresponds to the `/blog/:slug` route, in which case `params.slug` is available to the route
* The file `src/routes/index.svelte` (or `src/routes/index.md`, or `src/routes/index.js`) corresponds to the root of your app. `src/routes/about/index.svelte` is treated the same as `src/routes/about.svelte`.
* Files and directories with a leading underscore do *not* create routes. This allows you to colocate helper modules and components with the routes that depend on them — for example you could have a file called `src/routes/_helpers/datetime.js` and it would *not* create a `/_helpers/datetime` route

## Website structure/organization (TODO)

It's a structuring topic, as it will determine the navigation part. 

## Design and styling (TODO)

Nothing is done here, beside very crude and quick hacking of defaults.

* Most of the global styling should be done in `static/global.css`.
* but every page or component can have its own style too. Inside `<style>` tags for `*.svelte` files or inside `css style` fenced blocks in markdown files.

## PDF generation (TODO)

To be refined, but the plan could be to use a browser engine to scrape the content of the website and generating a PDF as a resulting process.

Refs :
* https://codeburst.io/high-quality-pdf-generation-using-puppeteer-5b51e2ab231a
* https://blog.risingstack.com/pdf-from-html-node-js-puppeteer/
* https://medium.com/@raphaelstaebler/advanced-pdf-generation-for-node-js-using-puppeteer-e168253e159c
* https://stackoverflow.com/questions/48510210/puppeteer-generate-pdf-from-multiple-htmls (leads for multipages)

**Beware :** Layouting print documents using HTML/CSS is still quite experimental and me need some tweaking depending on the needs.

## Publishing

Without any particular need on server side, Sapper can generate a static version, ready to be copied on a bare hosting platform.

See https://sapper.svelte.dev/docs#Exporting


## Go further :

* [Original Sapper boilerplate Readme](https://github.com/sveltejs/sapper-template/blob/master/README.md)
* [Sapper documentation website](https://sapper.svelte.dev/)

