# PHP CodeSniffer and WordPress Coding Standards with VS Code

_Last Updated 2020-07-31 by @tommcfarlin_

This guide is meant to provide all of the steps necessary to easily get up and running with PHP CodeSniffer, the WordPress Coding Standard ruleset, and Visual Studio Code.

![Visual Studio Code](https://tommcfarlin.com/wp-content/uploads/2020/07/visual-studio-code-974x1024.png)

All of the resources used in this guide are linked at the bottom. This guide is also licensed [MIT](https://github.com/tommcfarlin/phpcs-wpcs-vscode/blob/master/LICENSE). If you'd like to contribute, then please feel free to open issues or issue pull requests. I'll be happy to merge them and also add your username to [CONTRIBUTING](https://github.com/tommcfarlin/phpcs-wpcs-vscode/blob/master/CONTRIBUTING.md).

If you're looking for corresponding blog posts, please see:
1. [Setting Up PHP CodeSniffer in Visual Studio Code](https://tommcfarlin.com/php-codesniffer-in-visual-studio-code)
2. [Setting Up PHP CodeSniffer Per Project](https://tommcfarlin.com/php-codesniffer-per-project/)

As always, don't forget to checkout the [CHANGELOG](https://github.com/tommcfarlin/phpcs-wpcs-vscode/blob/master/CHANGELOG.md) to track everything that's changed since the initial release of this guide.

______

## 1. Verifying PHP

The following steps assume you have PHP installed and globally accessible on your system.
You can test this by entering the following command in the terminal:

```
$ php -v
```

And you should see something like this:

```
PHP 7.4.7 (cli) (built: Jun 12 2020 00:04:10) ( NTS )
Copyright (c) The PHP Group
Zend Engine v3.4.0, Copyright (c) Zend Technologies
    with Xdebug v2.9.6, Copyright (c) 2002-2020, by Derick Rethans
    with Zend OPcache v7.4.7, Copyright (c), by Zend Technologies
```

If you're looking for how to use a different version of PHP installed elsewhere on your system, this is not the guide for that. If, however, you're curious as to _where_ the version of PHP you're using is stored, you can enter:

```
$ which php
```

And you should see something similar to this:

```
/usr/local/bin/php
```

That should give you enough information for the rest of this guide.

## 2. Installing Composer

Installing Composer globally means that you'll be able to access it from anywhere on your system (that is, in any directory regardless of where you are). To do this, you can read the [manual](https://getcomposer.org/doc/00-intro.md) or follow the quick steps below (which summarize the manual, anyway):

1. Grab [the latest snapshot](https://getcomposer.org/composer.phar) of Composer. Save it somewhere you'll remember.
2. Move the file you just downloaded to the `/usr/local/bin/` directory on your machine.

To do this, open your terminal navigate to the directory where you downloaded `composer.phar`. Move the file to the diretory mentioned above by issuing the following command:

```
$ mv composer.phar /usr/local/bin/composer
```

And now you can access Composer from anywhere in your system. To do try it out, enter the following command in your terminal:

```
$ composer about
```

You should see something like this:

```
Composer - Package Management for PHP
Composer is a dependency manager tracking local dependencies of your projects and libraries.
See https://getcomposer.org/ for more information.
```

With Composer globally installed, you can now install the WordPress Coding Standards rules.

## 3. Installing PHP CodeSniffer

For the purposes of this document, we're installing PHP CodeSniffer on a project-by-project basis. To do this, we're going to be using Composer.

From the integrated terminal within Visual Studio Code, enter the following command:

```
$ composer require "squizlabs/php_codesniffer=3.*"
```

This will create `composer.json`, tell it where to locate the PHP CodeSniffer, and install it in a `vendor` directory. Once this is done, we need the WordPress Coding Standard ruleset.

## 4. Installing the WordPress Coding Standards Rules

I recommend placing the rules in a directory you can refer to often. Personally, I use a `projects` directory to manage all of my work.

From within your directory of choice, say `/projects`, enter the following command in the terminal:

```
$ composer create-project wp-coding-standards/wpcs:dev-master --no-dev
```

This will create a `wpcs` directory in your `projects` directory and it makes it easy to tell each project where the WordPress Coding Standards are stored because, remember, we'll be using Composer on a project-by-project basis.

## 5. Tell PHPCS About WPCS

From within Visual Studio's integrated terminal, make sure that you're in your project's directory and then issue the following command:

```
$ ./vendor/bin/phpcs --config-set installed_paths /path/to/dropbox/projects/wpcs
```

And this will tell your project's copy of PHPCS where the WordPress Coding Standards are.

## 6. Update User Settings

Finally, we need to let Visual Studio what we're going to be using to sniff out the code in our project and what rules to use. This is really easy to do. In Visual Studio, hit the `⌘,` (or whatever your operating system uses) command to open `settings.json`.

Make sure the file looks like the following (though you may need to tweak based on your existing settings)

```json
// Place your settings in this file to overwrite the default settings
{
    // PHPCS
    "phpcs.enable": true,
    "phpcs.standard": "WordPress",
    "phpcs.executablePath": "./vendor/bin/phpcs",
    "phpcs.showWarnings": true,
    "phpcs.composerJsonPath": "composer.json",
}
```

And this will enable PHPCS and will also tell it to use the standard WordPress ruleset. If this doesn't start working on the code your have automatically, then restart Visual Studio Code.
___

## Resources

- [Visual Studio Code](https://code.visualstudio.com/)
- [Getting Started](https://getcomposer.org/doc/00-intro.md)
- [The Latest Composer Snapshot](https://getcomposer.org/composer.phar)
- [PHP CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer)
- [WordPress Coding Standards](https://github.com/WordPress-Coding-Standards/WordPress-Coding-Standards)
- [Setting Up PHP CodeSniffer in Visual Studio Code](https://tommcfarlin.com/php-codesniffer-in-visual-studio-code)
- [Setting Up PHP CodeSniffer Per Project](https://tommcfarlin.com/php-codesniffer-per-project/)
