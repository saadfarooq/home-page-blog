---
layout: post
title: Setting up PhpUnit Testing with Yii and Composer
---

I decided to try [Composer](http://getcomposer.org/download/) for dependency management with our [Interlace](http://int.erlace.com) project. Composer itself is really easy to install and at least one of the installation options should work out.

Getting PhpUnit to work is a tad more annoying. Interlace uses Yii so we need the framework class as a dependency.

As per [this](http://stackoverflow.com/questions/17648066/composer-and-yii) question on StackOverflow, I use another project for the dependency because the main Yii project includes a lot of non-relevant stuff such as documentation, whereas we only need the framework folder.

    {
      "require": {
        "square1-io/yii-framework": "1.1.14"
      }
    }

When doing `composer install`, this installs the Yii-framework to the `vendor/square1-io/yii-framework`. The Yii `bootstrap.php` file (and your main project files) should now use this path to define the framework.
    
    <?php
      // change the following paths if necessary
      $yiit   = dirname(__FILE__).'/../../vendor/square1-io/yii-framework/yiit.php';
      $config = dirname(__FILE__).'/../config/test.php';

      require_once($yiit);
      require_once(dirname(__FILE__).'/WebTestCase.php');

      Yii::createWebApplication($config);
    ?>

Once that's running, there is the issue of PhpUnit. There are a bunch of dependencies in order to get it to work without any warnings or errors. I'll just list the `composer.json` instead of walking through each.

    {
      "require": {
          "square1-io/yii-framework": "1.1.14"
      }
      ,"require-dev": {
          "phpunit/phpunit": "3.7.*"
          ,"phpunit/phpunit-selenium": ">=1.2"
          ,"phpunit/php-invoker": "*"
          ,"phpunit/dbunit": ">=1.2"
          ,"phpunit/phpunit-story": "*"
      }
    }

A `composer install` (or `composer update` if this isnt' the first install) and you should be good. Tests can be run using the `phpunit` executable at `vendor/bin/phpunit`.

You might also want to remove the Internet Explorer link from the `phpunit.xml` file (unless you are using a Webdriver for it) or add others accordingly.

Now there's the problem of getting HTML reports. I have no idea why standard reporting (using the `--coverage-html` switch) produces a blank page. I'll update this if I find something.
