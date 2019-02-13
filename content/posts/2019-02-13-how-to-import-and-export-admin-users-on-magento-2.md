---
template: post
title: How to import and export admin users on Magento 2?
slug: How-import-and-export-admin-users-Magento2
draft: true
date: 2019-02-18T12:30:14.351Z
description: >-
  Check how you can move your admin users from one to another Magento 2
  installation without decrypting the password or change it.
category: Magento
tags:
  - Magento
  - Database
---
Your admin users data are on the tables **admin_user** and **admin_passwords** in your Magento 2 database, you can use these commands to export and then import in your second store:

**Export**

```
$ mysqldump -p --user=username dbname admin_user admin_passwords > myAdminUsers.sql
```

**Import**

```
$ mysql -u username -p -D dbname < myAdminUsers.sql
```

> **Important**
>
> If you use a database prefix, don't forget to use on these commands above.
