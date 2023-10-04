---
title: Progressive Web App
author: Priyesh Shrivastava
date: 2023-08-21
status: Research
references: https://dev.to/sabbir_zz/pwa-with-next-js-13-194l
type: R&D
tags:
    - '#PWA'
    - '#Javascript'
    - Technologies
---

# Progressive Web App

[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/) [![Netlify Status](https://api.netlify.com/api/v1/badges/d9934102-e0fb-4814-bcfc-9315e22a0c35/deploy-status)](https://app.netlify.com/sites/zeros-nextjs-pwa/deploys)

---

## Introduction

PWAs are applications built with web-technologies like HTML, CSS and JS but mimic the functionality and looks of a native application on the mobile devices. They can be installed just like and application using any modern browser on mobile as well as desktops.

## Benefits of PWA

-   Have Cross-platform compatibility.
-   They're fast and lightweight.
-   They work offline unlike other sites.
-   Push notifications functionality.
-   Low maintenance cost.

## Creating a PWA

For this example I will be using NextJS to create a PWA. The code for this already available on [this repository](https://github.com/priyesh-zero/nextjs-pwa).
It has been deployed on #netlify [here](https://zeros-nextjs-pwa.netlify.app/)

### Maniifest File

The manifest file contains the basic information about your application like:

-   App Name
-   App Icon
-   Splash Screen
-   Start URL
-   Theme Color
-   Display Mode
    It is this manifest file which lets the browser identify that the give application is a PWA and can be installed on users device.

The `manifest.json` file needs to be created at the root of the serving directory, so for React[^RE] project, it would be the `public` directory.

Below is a sample `manifest.json` file.

```json
{
    "theme_color": "#3b82f6",
    "background_color": "#f8fafc",
    "display": "standalone",
    "scope": "/",
    "start_url": "/",
    "name": "Your App Name",
    "short_name": "your_app_name",
    "description": "A PWA boilerplate with Next Js TypeScript",
    "icons": [
        {
            "src": "/icon-192x192.png",
            "sizes": "192x192",
            "type": "image/png"
        },
        {
            "src": "/icon-256x256.png",
            "sizes": "256x256",
            "type": "image/png"
        },
        {
            "src": "/icon-384x384.png",
            "sizes": "384x384",
            "type": "image/png"
        },
        {
            "src": "/icon-512x512.png",
            "sizes": "512x512",
            "type": "image/png"
        }
    ]
}
```

> This can also be generated using this [app](https://www.simicart.com/manifest-generator.html/)

### Linking the manifest file

The manifest file should be linked in the `<head>` of you application, for a React[^RE] project it would be the index.html file, for NextJS[^NJS], 12 and below need to create a `_document` file and add link tags, for 13 and above, it would be in the root layout file exporting metadata.

```ts
export const metadata: Metadata = {
    title: 'NextJS PWA',
    description: 'A NextJS application that implements PWA',
    manifest: '/manifest.json',
    themeColor: '#c29df1',
    icons: {
        apple: '/apple-icon.png',
    },
}
```

### PWA Configuration

To enable PWA a few configuration needs to be made. Using the worker files, the app needs to be registered. Now for base JS this can be done in the service-worker file.

To create a PWA for a vanilla JS[^JS] project here is an [extensive guide](https://web.dev/learn/pwa/), in which all the individual elements like caching, service workers, assets management are explored.

For NextJS[^NJS] simply include the following configuration files in the `next.config.js` file

```ts
/** @type {import('next').NextConfig} */

const withPWA = require('next-pwa')({
    dest: 'public',
    register: true,
    skipWaiting: true,
})

module.exports = withPWA({
    reactStrictMode: true,
})
```

### Adding .gitignore

During the application builds a few files will be created which is not required to be pushed to the repository, these files can be safely ignored by `git`[^GIT].

```
# Auto Generated PWA files
**/public/sw.js
**/public/workbox-*.js
**/public/worker-*.js
**/public/sw.js.map
**/public/workbox-*.js.map
**/public/worker-*.js.map
```

### Build and Test

This should create a basic PWA ready to be tested, for nextjs just run `yarn build` & `yarn start` and the hosted application should be PWA compatible.

[^RE]: #React
[^NJS]: #NextJS
[^JS]: #Javascript
[^GIT]: #git
