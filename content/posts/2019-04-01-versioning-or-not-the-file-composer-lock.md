---
template: post
title: Versioning or not the file composer.lock?
slug: /blog/versioning-or-not-the-file-composer-lock.html
draft: true
date: 2019-04-04T02:00:00.000Z
description: >-
  Many developers ignore the composer.lock into their .gitignore, it because
  it's an auto-generated file. By analyzing the gitignore file's purpose this
  theory is correct, however, is a good practice managing the version control of
  this file, and using the composer install command to prepare an environment,
  not composer update, let's check basis that sustains that idea in order to
  apply this change on your projects.
category: environment
tags:
  - environment
  - workflow
  - magento
---
Many developers ignore the composer.lock into their .gitignore, it because it's an auto-generated file. By analysing the .gitignore's purpose this theory is correct, however, is a good practice managing the version control of this file, and using the composer install command to prepare an environment, not composer update, let's check basis that sustains that idea in order to apply this change on your projects.

![Using or not the composer.lock file](https://i.imgur.com/Kl1Rs3A.png "Using or not the composer.lock file")

\- You can find in the [Composer documentation](https://getcomposer.org/doc/01-basic-usage.md#commit-your-composer-lock-file-to-version-control) saying:

> "You should commit the composer.lock file to your project repo so that all people working on the project are locked to the same versions of dependencies."

\- Having the composer.lock file, it will become the installation of composer dependencies **2x faster**.

\- You can let it more optimised using the parameters to optimize the autoload, to prefer the packages via source and avoiding getting the dev dependencies in a production environment.

\- As each install will use the composer.lock file, it will install the same package distribution version for each developer, avoiding the famous sentence **"It's working in my machine"**.

\- This practice is recommended for libraries too, according to the [Composer documentation](https://getcomposer.org/doc/02-libraries.md#lock-file).

> "For your library you may commit the composer.lock file if you want to."

\- Never use composer update in your production, it might update packages which you didn't update in UAT yet, so, UAT environment loses its purpose.

Are you versioning you composer.lock? let me know in the comments below!
