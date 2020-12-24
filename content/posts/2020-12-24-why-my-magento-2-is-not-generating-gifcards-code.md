---
template: post
title: Why my Magento 2 is not generating Gifcard's code?
slug: magento2-not-generating-giftcard-code
socialImage: /media/image-2.jpg
draft: false
date: 2020-12-24T21:09:29.340Z
description: Analyzing some orders workflow to a client we saw that in some
  orders the gift card code wasn't generated, so I decided to share here the
  solution that might help you too.
category: magento
tags:
  - tips&tricks
---
Analyzing some orders workflow to a client we saw that in some orders the gift card code wasn't generated. Inside the order's details, it was showing as below.

**Gift Card Accounts: N/A**

Analyzing the situation it was caused because of one specific payment method, it was set as Authorize only and not Authorize & Capture, the gif card code is generated only when the invoice is created.

So if you did a test order and didn't have the gift card code, try to invoice it, you will receive a new email with the code.

To check all the Giftcard codes generated you can go to the admin panel in **Marketing > Promotions > Gift Card Account**.

If you can you might able to fix it changing the payment method to Authorize & Capture or restricting the payment methods allowed to buy the gift cards.