---
title: laravel 部署优化
date: 2017-02-28 08:55:02
tags: [laravel,php]

---
做过 benchmark 的童鞋可能会发现 laravel 的性能(相对来说)其实很一般, 如果安装了各种扩展之后性能则会进一步下降...
当然, 就算是这种性能也可以满足绝大部分网站的要求了, 何况还有进一步优化的可能.

这篇文章就来简单讨论一下如何优化 laravel.
<!-- more -->

这里说的 laravel/lumen 是指的 5.x 版本
## 内置优化
### composer 的优化
```sh
composer install --optimize-autoloader --no-dev
```
这条命令安装依赖的时候不安装 dev 环境的依赖, 并且优化 `autoloader` 文件
我们也可以通过运行 `composer dump-autoload --optimize` 来手动生成优化文件
### .env 文件
部署项目的时候, 这个的配置文件中有两个值需要修改

```text
APP_ENV=production
APP_DEBUG=false
```
将 `APP_ENV` 设置为 `production` 对性能可能没有什么提升, 不过对某些 **重要操作** 的行为发生了变化, 比如执行 `migrate` 会要求我们确认执行
### laravel 的内置缓存
lavavel 内置了三条命令可以优化, 并且都是生成对应的缓存文件:

```sh
    # 生成 bootstrap/cache/config.php, 可以用 php artisan config:clear 删除缓存
    php artisan config:cache

    # 注意 routes 里面不能有 闭包路由!
    # 生成 bootstrap/cache/route.php, 可以用 php artisan route:clear 删除缓存
    php artisan route:cache

    # 生成 bootstrap/cache/compiled.php, 不过这个文件貌似只能手动删除了..
    # 生成的 compiled.php 文件相当大...可能反而造成载入慢?
    php artisan optimize --force
```

注意:
- 对应的缓存文件在 bootstrap/cache 里面, 这个目录里面的文件都可以自动生成, 但是不能 直接删除这个目录, 会造成错误
- `php artisan optimize --force` 这条命令使用之后反而有可能降低性能, 请自行测试后再决定是否使用!
- config 缓存生成之后, 如果安装了 **新依赖**, 应当先删除 config 缓存! 否则可能会无法载入新组件

### 关于 lumen
lumen 本身并没有提供优化命令, 但是其本身的性能已经相当高了


## 其他优化
### httpcache
如果网站内容并不需要实时更新, 使用 html缓存 是提升性能最有效的方法
laravel 本身并没有 html缓存, 不过有相关插件, 比如 [laravel-httpcache](https://github.com/barryvdh/laravel-httpcache)

经过本人简单测试 laravel 5.2 使用了缓存的页面性能基本已经和 没有任何优化的 lumen 5.2 的性能相当了(相同的数据查询, laravel 输出 html, lumen 输出 json)


## 参考
上面提到的方法都是比较简单又高效的方法
进一步的优化方式可以参考
- [https://github.com/neomerx/rhw-l5](https://github.com/neomerx/rhw-l5)
