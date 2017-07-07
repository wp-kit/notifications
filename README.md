# WPKit Notifications

This is a Wordpress PHP Component to handles both front-end and admin notifications This PHP Component was built to run within an Illiminate Container so is perfect for frameworks such as Themosis.

Often, Wordpress developers want to be able to use a single component the handle notifications stored in the session and their output to the client, usually after a redirect. 

In Wordpress we do have the ability to forge admin notices via some hooks but there a few hoops to jump through in that you have to write quite a bit of code to handle the session storage and the output, and currently there are no hooks for front-end notifications.

## Installation

If you're using Themosis, install via composer in the Themosis route folder, otherwise install in your theme folder:

```php
composer require "wp-kit/notifications"
```

## Registering Service Provider

**Within Themosis Theme**

Just register the service provider and facade in the providers config and theme config:

```php
//inside themosis-theme/resources/config/providers.config.php

return [
    Theme\Providers\RoutingService::class,
    WPKit\Notifications\NotificationServiceProvider::class
];
```

```php
//inside themosis-theme/resource/config/theme.config.php

'aliases' => [
    //
    'AdminNotifier' => WPKit\Notifications\Facades\AdminNotifier::class,
    'FrontEndNotifier' => WPKit\Notifications\Facades\FrontEndNotifier::class
    //
]
```

**Within functions.php**

If you are just using this component standalone then add the following the functions.php

```php
// within functions.php

// make sure composer has been installed
if( ! file_exists( __DIR__ . '/vendor/autoload.php' ) ) {
	
	wp_die('Composer has not been installed, try running composer', 'Dependancy Error');
	
}

// Use composer to load the autoloader.
require __DIR__ . '/vendor/autoload.php';

$container = new Illuminate\Container\Container(); // create new app container

$provider = new WPKit\Notifications\NotificationServiceProvider($container); // inject into service provider

$provider->register(); //register service provider
```


## Using Notifiers

WPKit Notifications are pretty flexible. You can use them anywhere but ideally you should use them in your Controllers. You can use the Facade or the Helper functions:

```php

use WPKit\Notifications\Facades\AdminNotifier;
use WPKit\Notifications\Facades\FrontEndNotifier;

// as php function as below

// using facade


```

## Handling the Output

```php

<some>

	<html></html>
	
</some>


```

## Requirements

Wordpress 4+

PHP 5.6+

## License

WPKit Notifications is open-sourced software licensed under the MIT License.