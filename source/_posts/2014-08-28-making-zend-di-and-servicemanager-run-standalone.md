---
layout: post
title: "Making Zend Di and ServiceManager run standalone"
description: "Successfully using ZF2's Di and ServiceManager outside a ZF2 MVC application"
category: php
tags: [php,zf2,di,notetomyself]
---
Setting up the Zend Framework 2 DiC and ServiceManager inside a ZF2 MVC application is done by the framework, you will only have to write your configuration array.

If you plan to use this components standalone, i. e. in your own software, you will not find one word about how to achieve this goal.

After digging through the application skelleton I found the solution below. Like in a MVC application the DiC works as a fallback to the ServiceManager instance, so you can ask the ServiceManager for a service only known to the Di container.

{% highlight php linenos %}
<?php

use Zend\Di;
use Zend\Mvc\Service\ServiceManagerConfig;
use Zend\ServiceManager\ServiceManager;
use Zend\ServiceManager\Di\DiAbstractServiceFactory;

/**
 * @see http://framework.zend.com/manual/2.3/en/modules/zend.service-manager.quick-start.html
 * @see http://framework.zend.com/manual/2.3/en/modules/zend.di.configuration.html
 */
$configuration = array(
    'definition'        => array(/* Zend\Di Configuration */),
    'service_manager'   => array(/* Zend\ServiceManager Configuration */),
);

$di = new Di\Di();
$di->configure(
    new Di\Config($configuration['definition'])
);

$service_manager = new ServiceManager(
    new ServiceManagerConfig($configuration['service_manager'])
);

$service_manager->addAbstractFactory(
    new DiAbstractServiceFactory($di)
);

{% endhighlight %}
