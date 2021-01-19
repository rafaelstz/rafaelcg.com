---
template: post
title: "Shopify API Release: January 2021"
slug: shopify-api-release-january-2021
socialImage: /media/image-2.jpg
draft: false
date: 2021-01-19T20:43:18.831Z
description: If you are a Shopify developer it's good to know the last updates,
  it includes features to use in your new app, deprecations to keep your app
  healthy, and the new possibilities to innovate. So let's check out the news
  for Q1.
category: shopify
tags:
  - tips&tricks
---
# 1º - Subscription APIs

A subscription is a business model that allows customers to pay a recurring price at scheduled intervals for goods or services. With subscription APIs, you can sell goods and services in multiple ways. For example, you can sell a product as a one-time purchase or as a recurring subscription.

The following diagram illustrates a high-level subscription flow for an app that has implemented a subscription flow using the product subscription app extension. As you can see you have many possibilities to bring subscription solutions to merchants, it includes management, automation and report apps.

![Shopify Subscription APIs](https://dev-to-uploads.s3.amazonaws.com/i/1juf1pjibmwbzahww15k.png) 

# 2º - Product Subscription App Extension

You can create this new kind of app extension called subscription using a single command from the Shopify App CLI, and it includes scaffolding for everything you need to start building an excellent merchant experience.

![Shopify Product Subscription App Extension](https://dev-to-uploads.s3.amazonaws.com/i/n97389s19j7pyzcguuri.png)
 

# 3º - Scheduled fulfillments

API clients can also reschedule fulfillment orders to a later date by using the new **fulfillmentOrderReschedule** mutation, and specifying a **fulfillAt** date in the future. Rescheduling a fulfillment order is especially helpful for prepaid subscriptions, when a customer may want to skip a shipment of consumable items like coffee or granola if they haven't run out.

# 4º - Automatic activation of app charges

This was my favorite improvement, billing for apps using the REST API was made in a three-step process:

- Step one: Create an application charge.
- Step two: The merchant accepts or declines the charge.
- Step three: If the charge is accepted, make an API call to activate the pending accepted charge.

If we didn't execute the last step we didn't have the charges applied to our clients, apps no longer need to perform that third step. Accepted application charges will automatically be transitioned into an “active” state, eliminating the possibility of charges that have been created by the app, accepted by the merchant, but then never activated and paid out to the partner.

# 5º - Financial reporting improvements

The 2021-01 version includes two changes to improve the accuracy of accounting apps.

First, TransactionFee is a new object available as a part of the API which includes much more detailed information about fees collected as a part of Shopify Payments payouts, including the flat rate charges, percentage charges, and a breakdown of the tax charged on these fees.

Second, API now includes tips received as a part of an order in both shop and presentment currencies using the totalTipReceivedSet field on the order object. This increased granularity will help accounting apps report even more accurately on fees and tips on any given order transaction.

Were you looking to have the 4º item as I was? Let me know which was your favorite item.