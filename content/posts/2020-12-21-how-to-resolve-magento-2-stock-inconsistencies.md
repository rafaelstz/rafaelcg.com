---
template: post
title: How to resolve Magento 2 stock inconsistencies?
slug: how-to-solve-magento2-stock-inconsistencies
socialImage: /media/image-2.jpg
draft: false
date: 2020-12-21T23:24:20.620Z
description: There are some issues that might cause the stock inconsistency
  issue, but before anything make sure you're running the most updated version
  of the MSI in your current Magento 2 installation, you can update it via
  Composer even not updating the entire Magento 2 installation.
category: magento
tags:
  - tips&tricks
  - magento
---
There are some issues that might cause the stock inconsistency issue, but before anything make sure you're running the most updated version of the MSI in your current Magento 2 installation, you can update it via Composer even not updating the entire Magento 2 installation.

## What causes reservation inconsistencies?

Inventory Management generates reservations for key events:

- Order placement (initial reservation)
- Order shipment (compensation reservation)
- Refund order or issue a credit memo (compensation reservation)
- Order cancellation (compensation reservation)

Reservation inconsistencies may occur when Inventory Management loses the initial reservation and enters too many reservation compensations (overcompensating and leading to inconsistent amounts), or correctly places the initial reservation but loses compensational reservations.

The following configurations and events can cause reservation inconsistencies:

- Upgrade Magento to 2.3.x with orders not in a completed state (Complete, Canceled, or Closed). - Inventory Management will create compensational reservations for these orders, but it will not enter or have the initial reservation that deducts from the salable quantity. We recommend using these commands after upgrading to Magento v2.3.x from 2.1.x or 2.2.x. If you have pending orders, the commands correctly update your salable quantity and reservations for sales and order fulfillment.
- You do not manage stock then later change this configuration. You may start using 2.3.x with Manage Stock set to "No" in the Magento configuration. Magento does not place reservations at order placement and shipment events. If you later enable the Manage Stock configuration and some orders were created at that time, the Salable Qty would be corrupted with compensation reservation when you handle and fulfill that order.
- You re-assign the Stock for a Website while orders submit to that website. The initial reservation enters for the initial stock and all compensational reservations enter the new stock.
- The sum total of all reservations may not resolve to 0. All reservations in the scope of an Order in a completed state (Complete, Canceled, Closed) should resolve to 0, clearing all salable quantity holds.

Reservations place a salable quantity hold for product SKUs per stock. When you ship, add products, cancel, or refund an order, compensation reservations enter to place or clear these holds.

## Resolve reservations inconsistencies

MSI provides two CLI commands to check and resolve reservation inconsistencies:

- `inventory:reservation:list-inconsistencies`
- `inventory:reservation:create-compensations`

References: [Magento CLI Reference][1]


  [1]: https://github.com/magento/inventory/wiki/CLI-Reference

