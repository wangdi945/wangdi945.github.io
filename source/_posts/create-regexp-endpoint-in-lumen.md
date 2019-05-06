---
title: create regexp endpoint in lumen
date: 2019-05-06 21:02:59
tags:
---
# lumen使用正则表达式定义路由
lumen不支持使用正则表达式定义路由。但是lumen支持可以通过在路由定义中使用正则表达式来约束路由参数的格式：

```php
$router->get('user/{name:[A-Za-z]+}', function ($name) {
    //
});
```

因此可以使用比较hack的方式实现正则表达式定义：

```php
$router->get('{uri:.*}', function () {
    //
});
```

dingo也支持这种方式：
```php
$api->any('{uri:.*}', function () {
    //
});
```

# 参考
https://laraveldaily.com/routes-file-redirect-everything-else-to-homepage/