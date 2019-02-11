---
template: post
title: Configure a local Magento 2 multi-store
slug: /blog/Magento-2-multistore-local.html
draft: false
date: "2019-01-25T21:40:32.169Z"
description: >-
  An Essay on Typography by Eric Gill takes the reader back to the year 1930.
  The year when a conflict between two worlds came to its term. The machines of
  the industrial world finally took over the handicrafts.
category: Magento
tags:
  - Magento
---
When we have to configure a multi-store in your local machine you can configure the local NGINX or Apache configuration to make it work, or you can quickly change your `index.php` just to test, fix the issues and not commit this change.

In this same case just to test using Magento 1 we used to change the `$mageRunCode` and `$mageRunType` in the **.htaccess** or **httpd.conf.**

In Magento 2 to test quickly you can use that code into your `index.php`:

```php
$params = $_SERVER;
$params[\Magento\Store\Model\StoreManager::PARAM_RUN_CODE] = 'website_code';
$params[\Magento\Store\Model\StoreManager::PARAM_RUN_TYPE] = 'website';
$bootstrap = \Magento\Framework\App\Bootstrap::create(BP, $params);
```
