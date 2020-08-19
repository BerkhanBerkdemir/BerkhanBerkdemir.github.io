---
title: Bootstrap 4 CSS and Symfony
date: 2018-02-07
updated: 2018-03-25
layout: post
---

Hello guys,

I'm writing about this topic because I migrated my old projects to Symfony 4. These days I used to use assetic which is based on pure PHP. It was easy to use and I learned assetic mechanism in one week.

Now, Symfony team changed the rules and they are using now JavaScript based webpack. They renamed the product name to **Encore**. I started 1 month ago to use. Actually, I understand little bit how this is working. I'll share my first Bootsrap experience rest of you.

## Install encore with composer
```bash
composer require encore
```

It is so easy to install but usage little bit different.

## Install bootstrap with NPM
I have NPM that's why I'll use NPM package management system. You can use yarn. Actually symfony offical documents using yarn.

```bash
npm install --only=dev bootstrap
```

Why `--only=dev`? Because I'll use only development stage after that I'll send to CDN (This article doesn't show CDN uploading).

## Install node SASS dependencies
If you want to run encore, you will get an error about node sass package.

Let's download it.

```bash
npm install --only=dev node-sass sass-loader
npm install #Install other stuff for ready to use.
```

You have to have those package. If you don't have you cannot use webpack feature.

## Write SCSS/SASS or CSS file
This is easy. Let's see how.

```scss
/* assets/index.scss */
@import "../node_modules/bootstrap/scss/bootstrap-reboot";
@import "../node_modules/bootstrap/scss/bootstrap";
```

That's it. Not big deal, right?

We just added bootstrap core SCSS files to index SCSS file. After that we will compile it. Also, you can your custom CSS or another CSS, SASS/SCSS file into this `index.scss` file

## Configure webpack.config.js
```javascript
// webpack.config.js

var Encore = require('@symfony/webpack-encore');

Encore
    // the project directory where compiled assets will be stored
    .setOutputPath('public/build/')
    // the public path used by the web server to access the previous directory
    .setPublicPath('/public/build')
    .cleanupOutputBeforeBuild()
    .enableSourceMaps(!Encore.isProduction())
    // uncomment to create hashed filenames (e.g. app.abc123.css)
    .enableVersioning(Encore.isProduction())

    // uncomment to define the assets of the project
    // .addEntry('js/app', './assets/js/app.js')
    // .addStyleEntry('css/app', './assets/css/app.sss')
    .addStyleEntry('css/index', './assets/index.scss')

    // uncomment if you use Sass/SCSS files
    .enableSassLoader()

    // uncomment for legacy applications that require $/jQuery as a global variable
    //.autoProvidejQuery()
;

module.exports = Encore.getWebpackConfig();
```

What is that?!??!?

This is my basic Webpack config file. The file enable SASS/SCSS, source mapping and also versioning. If you don't have any idea with versioning, just google it, and turn back to read.

## Reconfigure framework.yml

```yaml
# config/packages/framework.yaml

framework:
    assets:
        # feature is supported in Symfony 3.3 and higher
        json_manifest_path: '%kernel.project_dir%/public/build/manifest.json'
```

Why do you need to add this line? First of all, you have to do this but why?

If you are in production stage and you use versioning. Can you imagine that, you have `index.jd82djaskd01kalsd32.css` file, and this is your index file. Each deployment you have to change it.

If we added this line, Symfony will say this path or alias name to our router.

## Install asset with composer
```bash
composer require asset
```

We will use asset for templating. It is easy to use integrate CSS/JS to your twig/html files.

## Write your first template
First of all I won't show you to create any router or controller. I just show you these twig files

{% raw %}
```
{# templates/base.html.twig #}
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>{% block title %}Welcome!{% endblock %}</title>
        {% block stylesheets %}{% endblock %}

    </head>
    <body>
        {% block body %}{% endblock %}

        {% block javascripts %}{% endblock %}

    </body>
</html>
```
{% endraw %}

{% raw %}
```
{# templates/index.html.twig #}
{% extends "base.html.twig" %}

{% block stylesheets %}<link rel="stylesheet" href="{{ asset('build/index.css') }}"/>{% endblock %}

{% block body %}<h1>Hello, World!</h1>{% endblock %}
```
{% endraw %}


You will render `index.html.twig` file into your controller.

## Run it
Now, we don't have any CSS file. How will we create it?

```bash
node_modules/.bin/encore dev
```

## Serve it (Optional)
You can use symfony/server or php built in server. I'll show you both way.

### Serve your project with symfony/server

```bash
composer require server --dev
php bin/console server:run
```

This package benefits, if already taken 8000 port it will try chance with 8001 and so on. Also real time you can see what is going on (like http access, 200, 404...).

### Serve your project with PHP Built-in server

> PHP Built-in server can occur an error. May be you cannot see the assets. Please use Symfony/Server

```bash
php -S 127.0.0.1:8000 -t public/ public/index.php
```

But, I recomended first way. And you will see this beatiful page

![Bootstrap 4 and Symfony](https://i.imgur.com/nlB3OCY.png)

## Conclusion
Now, you can see this steps and you can think this is easy than assetic maybe another asset management system. But, I stuck and I just wrote for beginner user (They can think this is hard way to use).

Anyway, if you have any question/recommended feel free to use disqus.

Happy codding.
