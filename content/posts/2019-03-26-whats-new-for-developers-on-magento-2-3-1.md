---
template: post
title: What's new for developers on Magento 2.3.1
slug: /blog/whats-new-for-developers-on-magento2-3-1.html
draft: false
date: 2019-03-27T17:26:00.000Z
description: >-
  Check out what is new on the new for developers on the new Magento 2.3.1
  released today, it includes 200 functional fixes and 30 security enhancements.
  You may know the updates about GraphQL, Inventory Management, PWA, inventory
  management and more.
category: Magento
tags:
  - Magento
---
Today Magento is launching the Magento 2.3.1, and in each new release, I consider important to every developer now which components were more changed. This release includes over 200 functional fixes to the core product, over 500 pull requests contributed by the community, and over 30 security enhancements. These contributions range from minor clean-up of core code to the development of substantial features such as Inventory Management and GraphQL.



# Highlights



## Developer experience news

#### Automation of upgrade process

A new composer plugin `magento/composer-root-update-plugin` automatically updates all dependencies in composer.json during a Magento 2.x upgrade.

#### Other improvements

The packages [PWA Studio](https://magento-research.github.io/pwa-studio/) and [GraphQL](https://devdocs.magento.com/guides/v2.3/graphql/release-notes.html) were updated.



## Security news

We have 30 security enhancements that help close:

* Cross-site scripting
* Arbitrary code execution
* Sensitive data vulnerabilities

You can check them into [Magento Security Center](https://magento.com/security/patches/magento-2.3.1-2.2.8-and-2.1.17-security-update).



## Performance news

* The shipping and billing data that a user enters during checkout nows persists if the user interrupts checkout to continue shopping. Previously, checkout data was deleted after a cart update.
* The UI components from customer address have been rewritten for supporting the management of customers with 3000 and more address.
* The admin order creation page now handles customer accounts with 3000 addresses without performance issues.
* The customer address book shows via grid on the storefront the list of additional customer addresses.



## DevOps news

* Magento supports Elasticsearch 6.0
* Magento supports Redis 5.0
* Magento supports PHP 7.2.x



## Merchant tool news

#### Admin order creation

The admin order creation workflow now eliminates delays to edit billing and shipping addresses, and these fields are populating just when populated.

#### PDP images

Large PDP images (larger than 1920 x 1200) uploaded by merchants will not be compressed anymore, the high quality is kept.

#### Inventory Management 1.1.0

Now the community project [Multi-Source Inventory](https://devdocs.magento.com/guides/v2.3/inventory/release-notes.html) (MSI) has added multiple new features:

* **Support for Elasticsearch and Inventory Management**, all site searches now return correct products and quantities when Elasticsearch is used.
* **Distance-priority source selection**, using Google Maps API it will fulfill costs based on the closest inventory location.
* **Mass inventory transfer**, Bulk transfer of inventory has been optimized
* **In-store pickup fulfillment option**, the merchant can enable in-store pickup for selected sources.

If you want to know more details about all the issues which were fixed check the [DevDocs Release](https://devdocs.magento.com/guides/v2.3/release-notes/ReleaseNotes2.3.1OpenSource.html#fixed-issues).
