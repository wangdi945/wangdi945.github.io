---
title: create lumen project
date: 2019-05-05 10:17:09
tags:
---
# 介绍
Lumen + dingo快速搭建API服务。

# 创建项目
```bash
composer create-project --prefer-dist laravel/lumen new_project
```
# 安装Dingo
为了安装这个包你需要：

- PHP ^7.0

在项目中修改`composer.json`文件，运行`composer update`加载最新版本的包。

```json
"require": {
    "dingo/api": "^2.2"
}
```

# 注册服务
如果你使用Lumen，请打开`bootstrap/app.php`并注册服务提供者：

```php
$app->register(Dingo\Api\Provider\LumenServiceProvider::class);
```

# 配置
```
API_STANDARDS_TREE=vnd
API_SUBTYPE=myapp
API_DOMAIN=api.myapp.com
API_VERSION=v1
API_NAME="My API"
API_CONDITIONAL_REQUEST=false
API_STRICT=false
API_DEFAULT_FORMAT=json
API_DEBUG=true
```

# 路由
```php
$api = app('Dingo\Api\Routing\Router');
$api->version('v1', [], function ($api) {
    $api->group(['namespace' => 'App\Http\Controllers'], function ($api) {
        $api->any('/', function () {return app()->version();});
    });
});
```

# 参考
https://juejin.im/post/5b544f19f265da0fac1e149d
https://github.com/liyu001989/lumen-api-demo