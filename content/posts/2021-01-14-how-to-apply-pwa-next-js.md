---
template: post
title: How to apply PWA + Next JS
slug: setup-pwa-nextjs-app
socialImage: /media/image-2.jpg
draft: false
date: 2021-01-14T17:51:43.274Z
description: "The faster way to set up and utilize PWA in your Next JS
  application, check examples and tips to achieve it in minutes preparing your
  application from stretch and getting it ready for production. "
category: javascript
tags:
  - tips&tricks
  - pwa
  - javascript
  - nextjs
---
When starting with [Next framework](https://nextjs.org/) probably you're going to start setting up a basic landing page or some kind of concept prove, seeing how simple it's to have PWA on it.

If you're creating your project now you can just run this command below, then it's going to create a boilerplate of a simple Next project.

```
npx create-next-app
```
Checking the folder you will be able to see a complete project ready to be customized and tested, just running `npm run dev`.

## Setup PWA

The first thing to install is the package **next-pwa**, to them add a new configuration that makes the application create the required service worker files during the compilation. To finish you will need to create files with the project's configuration.

Let's start creating the `next.config.js` when putting this content below.

```
const withPWA = require('next-pwa')
 
module.exports = withPWA({
    pwa: {
        dest: 'public'
    }
})
```

This file is going to say to Next to generate the required files in the **public** folder.
One of the files that we need to create to specify the project's properties is the **manifest.json**, it'll be in the `public` folder and you can generate it here:

[App Manifest Generator](https://app-manifest.firebaseapp.com/)

Your application must have some meta tags to specify the icons, theme color and etc. To have all the head information you can create a file `components/header.js` and put this content like below.

```
import Head from 'next/head'

function Header() {
   return(
    <Head>
      <meta charset='utf-8' />
      <meta http-equiv='X-UA-Compatible' content='IE=edge' />
      <meta name='viewport' content='width=device-width,initial-scale=1,minimum-scale=1,maximum-scale=1,user-scalable=no' />
      <meta name='description' content='Description' />
      <title>Next.js PWA</title>

      <link rel='manifest' href='/manifest.json' />
      <link href='/favicon-16x16.png' rel='icon' type='image/png' sizes='16x16' />
      <link href='/favicon-32x32.png' rel='icon' type='image/png' sizes='32x32' />
      <link rel='apple-touch-icon' href='/apple-icon.png'></link>
      <meta name='theme-color' content='#333333' />
    </Head>
   )
}
export default Header
```

To generate the favicons you can use this online tool.

[Favicon & App Icon Generator](https://www.favicon-generator.org/)

After that you just need to run the command `npm run dev`, you will be able to have a PWA application running and saving the cache via service workers in your browser.

## Tips

- It's not needed to have the favicons generated to have the service workers working and ready to be tested.
- Compare your code with the code in the [next-js-pwa-example](https://github.com/skolhustick/next-js-pwa-create-next-app/tree/master).
- Utilize HTTPS to test it.