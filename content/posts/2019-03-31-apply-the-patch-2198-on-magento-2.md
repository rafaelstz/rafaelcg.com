---
template: post
title: Apply the patch 2198 on Magento 2
slug: /blog/avoid-sql-injection-check-how-to-apply-the-patch2198-Magento2.html
draft: true
date: 2019-03-31T05:34:40.532Z
description: >-
  Magento Commerce and Open Source 2.3.1, 2.2.8 and 2.1.17 contain multiple
  security enhancements that help close Remote Code Execution (RCE), Cross-Site
  Scripting (XSS) and other vulnerabilities, one of these security fixes avoid
  SQL Injection which can do anything on your database, check more details
  below.
category: Magento
tags:
  - Magento
---
Magento Commerce and Open Source 2.3.1, 2.2.8 and 2.1.17 contain multiple security enhancements that help close Remote Code Execution (RCE), Cross-Site Scripting (XSS) and other vulnerabilities, one of these security fixes avoid SQL Injection which can do anything on your database, check more details below.
## PRODSECBUG-2198: SQL Injection vulnerability through an unauthenticated user
**Severity:** 9
**Description:** An unauthenticated user can execute arbitrary code through an SQL injection vulnerability, which causes sensitive data leakage.
**Products affected:** Magento Open Source prior to 1.9.4.1, and Magento Commerce prior to 1.14.4.1, Magento 2.1 prior to 2.1.17, Magento 2.2 prior to 2.2.8, Magento 2.3 prior to 2.3.1
**Fixed In: **Magento Open Source 1.9.4.1, Magento Commerce 1.14.4.1, SUPEE-11086, Magento 2.1.17, Magento 2.2.8, Magento 2.3.1 
# How to apply?
1- Require composer-patches: 

```
composer require cweagans/composer-patches
```

2 - Create a folder called **m2-hotfix** in your project's root folder, then add the files below there, it's split into two files because each one affects a different core module. This files are for Magento 2.2.x, if you are using Magento 2.1.x or 2.3.x, you can download the patch and split the files per file changed as it's below.

_PRODSECBUG-2198-2.2-CE-2019-03-25-08-43-16-framework.patch_

```

diff --git a/DB/Adapter/Pdo/Mysql.php b/DB/Adapter/Pdo/Mysql.php
index 1449d6d..38085a3 100644
--- a/DB/Adapter/Pdo/Mysql.php
+++ b/DB/Adapter/Pdo/Mysql.php
@@ -2904,7 +2904,7 @@ class Mysql extends \Zend_Db_Adapter_Pdo_Mysql implements AdapterInterface
                 if (isset($condition['to'])) {
                     $query .= empty($query) ? '' : ' AND ';
                     $to     = $this->_prepareSqlDateCondition($condition, 'to');
-                    $query = $this->_prepareQuotedSqlCondition($query . $conditionKeyMap['to'], $to, $fieldName);
+                    $query = $query . $this->_prepareQuotedSqlCondition($conditionKeyMap['to'], $to, $fieldName);
                 }
             } elseif (array_key_exists($key, $conditionKeyMap)) {
                 $value = $condition[$key];
-- 
2.7.4

```



_PRODSECBUG-2198-2.2-CE-2019-03-25-08-43-16-module-catalog.patch_

```

diff --git a/Model/Product/ProductFrontendAction/Synchronizer.php b/Model/Product/ProductFrontendAction/Synchronizer.php
index 7a1926c..331c667 100644
--- a/Model/Product/ProductFrontendAction/Synchronizer.php
+++ b/Model/Product/ProductFrontendAction/Synchronizer.php
@@ -138,7 +138,9 @@ class Synchronizer
         $productIds = [];
 
         foreach ($actions as $action) {
-            $productIds[] = $action['product_id'];
+            if (isset($action['product_id']) && is_int($action['product_id'])) {
+                $productIds[] = $action['product_id'];
+            }
         }
 
         return $productIds;
@@ -159,33 +161,37 @@ class Synchronizer
         $customerId = $this->session->getCustomerId();
         $visitorId = $this->visitor->getId();
         $collection = $this->getActionsByType($typeId);
-        $collection->addFieldToFilter('product_id', $this->getProductIdsByActions($productsData));
-
-        /**
-         * Note that collection is also filtered by visitor id and customer id
-         * This collection shouldnt be flushed when visitor has products and then login
-         * It can remove only products for visitor, or only products for customer
-         *
-         * ['product_id' => 'added_at']
-         * @var ProductFrontendActionInterface $item
-         */
-        foreach ($collection as $item) {
-            $this->entityManager->delete($item);
-        }
-
-        foreach ($productsData as $productId => $productData) {
-            /** @var ProductFrontendActionInterface $action */
-            $action = $this->productFrontendActionFactory->create([
-                'data' => [
-                    'visitor_id' => $customerId ? null : $visitorId,
-                    'customer_id' => $this->session->getCustomerId(),
-                    'added_at' => $productData['added_at'],
-                    'product_id' => $productId,
-                    'type_id' => $typeId
-                ]
-            ]);
-
-            $this->entityManager->save($action);
+        $productIds = $this->getProductIdsByActions($productsData);
+
+        if ($productIds) {
+            $collection->addFieldToFilter('product_id', $productIds);
+
+            /**
+             * Note that collection is also filtered by visitor id and customer id
+             * This collection shouldn't be flushed when visitor has products and then login
+             * It can remove only products for visitor, or only products for customer
+             *
+             * ['product_id' => 'added_at']
+             * @var ProductFrontendActionInterface $item
+             */
+            foreach ($collection as $item) {
+                $this->entityManager->delete($item);
+            }
+
+            foreach ($productsData as $productId => $productData) {
+                /** @var ProductFrontendActionInterface $action */
+                $action = $this->productFrontendActionFactory->create([
+                    'data' => [
+                        'visitor_id' => $customerId ? null : $visitorId,
+                        'customer_id' => $this->session->getCustomerId(),
+                        'added_at' => $productData['added_at'],
+                        'product_id' => $productId,
+                        'type_id' => $typeId
+                    ]
+                ]);
+
+                $this->entityManager->save($action);
+            }
         }
     }


```

3 - Add a patches section in your _composer.json_.

```
{
  "require": {
    "cweagans/composer-patches": "^1"
  },
  "extra": {
    "patches": {
      "magento/framework": {
        "PRODSECBUG-2198": "https://gist.githubusercontent.com/barryvdh/8bf1ba88e4a7bfe3ad007de8dbf2600c/raw/e8d7e0072990cafbcba0e847b20fce62d8793938/PRODSECBUG-2198-2.2-CE-2019-03-25-08-43-16-framework.patch"
      },
      "magento/module-catalog": {
        "PRODSECBUG-2198": "https://gist.githubusercontent.com/barryvdh/8bf1ba88e4a7bfe3ad007de8dbf2600c/raw/e8d7e0072990cafbcba0e847b20fce62d8793938/PRODSECBUG-2198-2.2-CE-2019-03-25-08-43-16-module-catalog.patch"
      }
    }
  }
}
```


4 - Remove the packages which will be affected.

```
rm -rf vendor/magento/module-catalog vendor/magento/framework composer.lock
composer install

```
## Done
Thank you for read it!

## Check too:
[Magento 2.3.1, 2.2.8 and 2.1.17 Security Update](https://magento.com/tech-resources/download#download2288)
[MAGENTO 2.2.0 <= 2.3.0 UNAUTHENTICATED SQLI](https://www.ambionics.io/blog/magento-sqli)
[Barry's Gist](https://gist.github.com/barryvdh/8bf1ba88e4a7bfe3ad007de8dbf2600c)
