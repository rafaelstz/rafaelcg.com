---
template: post
title: 'Magento 2:  cache clean vs cache flush'
slug: magento2-cache-clean-or-cache-flush
draft: false
date: 2019-02-14T11:00:00.000Z
description: "Do you know the difference between cache:clean and cache:flush on Magento 2? In this post I'll explain the main difference and when is the best moment to use each one."
category: Magento
socialImage: "/media/image-2.jpg"
tags:
  - Magento
  - development
---
During the development we constantly use the Magento feature to clean or flush the cache, but do you know the difference? Check it out this difference based on DevDoc.

**php bin/magento cache:clean**

Cleaning a cache type deletes all items from enabled Magento cache types only. In other words, this option does not affect other processes or applications because it cleans only the cache that Magento uses.

> Disabled cache types are not cleaned.

**php bin/magento cache:flush**

Flushing a cache type purges the cache storage, which might affect other processes applications that are using the same storage.

**Reference:** [DevDocs Manage the cache](https://devdocs.magento.com/guides/v2.3/config-guide/cli/config-cli-subcommands-cache.html)
