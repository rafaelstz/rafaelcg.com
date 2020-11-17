---
template: post
title: Shopify App CLI
slug: shopify-app-cli
draft: false
date: 2020-11-17T15:41:02.212Z
description: >-
  If you are going to start developing Shopify Apps the Shopify CLI is one of
  the tools that will optimize a lot your workflow, mainly if you are creating a
  NodeJS or Ruby on Rails app. You can install it on Linux, macOS or Windows 10,
  I used it in my MacOs via Homebrew, if you use Linux or macOS these
  descriptions bellow will be exactly what you need to know, on Windows you
  might have some headaches because you will need to install RubyInstaller for
  Windows or some VM.
category: shopify
tags:
  - shopify
---
If you are going to start developing Shopify Apps the Shopify CLI is one of the tools that will optimize a lot your workflow, mainly if you are creating a NodeJS or Ruby on Rails app.

You can install it on Linux, macOS or Windows 10, I used it in my MacOs via Homebrew, if you use Linux or macOS these descriptions bellow will be exactly what you need to know, on Windows you might have some headaches because you will need to install [RubyInstaller for Windows](https://rubyinstaller.org/downloads/) or some VM.

![Shopify App CLI](https://i.imgur.com/tcEmFqf.png "Shopify App CLI")

# Installing Shopify CLI ⚡️

The process to install it and configure it is very simple, as soon as you have the requirements you can set it up in minutes.

## Requirements

* [Shopify partner account](https://partners.shopify.com/signup)
* [Shopify development store](https://help.shopify.com/en/partners/dashboard/development-stores#create-a-development-store) to install and test apps
* [Ruby](https://www.ruby-lang.org/) 2.5.1+

## macOS

```
$ brew tap shopify/shopify
$ brew install shopify-cli
```

## Debian/Ubuntu Linux

1. Download the .deb file from the [releases page](https://github.com/Shopify/shopify-app-cli/releases)
2. Install the downloaded file


```
$ sudo apt install /path/to/downloaded/shopify-cli-x.y.z.deb
```

## CentOS 8+/Fedora/Red Hat/SUSE Linux

1. Download the .rpm file from the [releases page](https://github.com/Shopify/shopify-app-cli/releases)
2. Install the downloaded file


```
$ sudo yum install /path/to/downloaded/shopify-cli-x.y.x.rpm
```

# Start to use it 👨‍💻

The first step is to create our app automatically via the Shopify CLI, the CLI will ask you some questions, like what's the store that you would like to install it, which Shopify Partner account would you like to use. As soon as you have your base app created you can access the app folder and run the command to start the local server to test it.

1. Create the app in your terminal.


```
$ shopify create
```

2. Start it.


```
$ shopify serve
```

# Core commands

These below are all the commands available to you to use after creating the NodeJS app like mine.

**connect:** Connect (or re-connect) an existing project to a Shopify partner organization and/or a store. Creates or updates the .env file, and creates the .shopify-cli.yml file.

  _Usage: shopify connect_

**create:** Create a new project.

  _Usage: shopify create \[ node | rails ]_

**logout:** Log out of a currently authenticated partner organization and store, or clear invalid credentials

  _Usage: shopify logout_

**version:** Prints version number.

  _Usage: shopify version_

**deploy:** Deploy the current Node project to a hosting service. Heroku (https://www.heroku.com) is currently the only option, but more will be added in the future.

  _Usage: shopify deploy \[ heroku ]_

**generate:** Generate code in your Node project. Supports generating new billing API calls, new pages, or new webhooks.

  _Usage: shopify generate \[ billing | page | webhook ]_

**open:** Open your local development app in the default browser.

  _Usage: shopify open_

**populate:** Populate your Shopify development store with example customers, orders, or products.

  _Usage: shopify populate \[ customers | draftorders | products ]_

**serve:** Start a local development node server for your project, as well as a public ngrok tunnel to your localhost.

  _Usage: shopify serve_

**tunnel:** Start or stop an http tunnel to your local development app using ngrok.

  _Usage: shopify tunnel \[ auth | start | stop ]_

# Thank you

Let me know what do you think of this CLI if you have used it, if you had some difficulties you can check the original [Shopify documentation](https://shopify.github.io/shopify-app-cli/) about it.
