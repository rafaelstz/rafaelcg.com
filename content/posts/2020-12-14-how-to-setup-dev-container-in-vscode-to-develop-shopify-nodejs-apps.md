---
template: post
title: How to setup Dev Container in VSCode to develop Shopify nodejs apps
slug: setup-devcontainer-vscode-shopify-node-app
socialImage: /media/image-2.jpg
draft: true
date: 2020-12-14T16:56:35.247Z
description: >-
  Learn how to start to use a new Docker environment via DevContainer in order
  to have a better environment to work with your Shopify apps in NodeJS using
  VSCode. With the files provided, you can specify the NodeJS and Shopify CLI
  version.
category: shopify
tags:
  - tips&tricks
---
If you work with VSCode and have your local environment directly in your machine I recommend starting to looking Docker, it's an easy way to have your app running in a virtualized environment with its own OS and packages to each app.

## Advantages

\- Work in an environment exactly as production.

\- Don't install all the packages to all projects directly on your machine.

\- Be more productive, avoiding issues and mistakes with node version or Shopify CLI version.


## How to start

You just need to create these two files in your project's root folder.

**.devcontainer/devcontainer.json**

```
{
  "name": "Node.js",
  "build": {
    "dockerfile": "Dockerfile",
    // Update 'VARIANT' to pick a Node version: 10, 12, 14
    "args": {"VARIANT": "14", "SHOPIFYCLI": "1.5.0"}
  },

  // Set *default* container specific settings.json values on container create.
  "settings": {
    "terminal.integrated.shell.linux": "/bin/bash"
  },

  // Add the IDs of extensions you want installed when the container is created.
  "extensions": ["dbaeumer.vscode-eslint"],

  // Use 'forwardPorts' to make a list of ports inside the container available locally.
  "forwardPorts": [80, 3456, 4040],

  // Use 'postCreateCommand' to run commands after the container is created.
  "postCreateCommand": "npm install",

  // Comment out connect as root instead. More info: https://aka.ms/vscode-remote/containers/non-root.
  "remoteUser": "node"
}
```

**.devcontainer/Dockerfile**

```
ARG VARIANT="14-buster"

FROM mcr.microsoft.com/vscode/devcontainers/javascript-node:0-${VARIANT}

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends ruby

ARG SHOPIFYCLI="1.5.0"

RUN wget https://github.com/Shopify/shopify-app-cli/releases/download/v${SHOPIFYCLI}/shopify-cli-${SHOPIFYCLI}.deb \
    && sudo apt install ./shopify-cli-${SHOPIFYCLI}.deb && rm ./shopify-cli-${SHOPIFYCLI}.deb
```

To finish it, you just need to open your VSCode and type `CMD + Shift + P` and execute the command below.

    > Remote-Containers: Open Folder in Container
