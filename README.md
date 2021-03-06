# Mobizon notifications channel for Laravel 5.3+

[![Latest Version on Packagist](https://img.shields.io/packagist/v/laraketai/mobizon.svg?style=flat-square)](https://packagist.org/packages/laraketai/mobizon)
[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE.md)
[![StyleCI](https://styleci.io/repos/163982456/shield)](https://styleci.io/repos/163982456)
[![Total Downloads](https://img.shields.io/packagist/dt/laraketai/mobizon.svg?style=flat-square)](https://packagist.org/packages/laraketai/mobizon)


This package makes it easy to send SMS notifications using [Mobizon](https://mobizon.kz) with Laravel 5.3.

## Contents

- [Installation](#installation)
	- [Setting up the Mobizon service](#setting-up-the-Mobizon-service)
- [Usage](#usage)
	- [Available Message methods](#available-message-methods)
- [Changelog](#changelog)
- [Testing](#testing)
- [Security](#security)
- [Contributing](#contributing)
- [Credits](#credits)
- [License](#license)


## Installation

You can install this package via composer:
```
composer require laraketai/mobizon
```

Laravel 5.5 < Add the service provider to  `config/app.php`:

```php
// config/app.php
'providers' => [
    ...
    Laraketai\Mobizon\MobizonServiceProvider::class,
],
```

Publish Config File `config/mobizon.php`:
```
php artisan vendor:publish --provider="Laraketai\Mobizon\MobizonServiceProvider"
```


### Setting up your Mobizon service
Log in to your [Mobizon](https://mobizon.kz/help/api-docs/sms-api) and grab your Api, Api Secret Key. Add them to `config/services.php`.  

```php
// config/mobizon.php
...
'mobizon' => [
    'alphaname' => null, //Optional, if you don't have registered alphaname, just skip this param and your message will be sent with our free common alphaname.
    'secret' => env('MOBIZON_APP_KEY'), // Your secret API key
],
```

## Usage

Follow Laravel's documentation to add the channel your Notification class:

```php
use Illuminate\Notifications\Notification;
use Laraketai\Mobizon\MobizonChannel;
use Laraketai\Mobizon\MobizonMessage;

public function via($notifiable)
{
    return [MobizonChannel::class];
}

public function toMobizon($notifiable)
{
    return MobizonMessage::create("Task #{$notifiable->id} is complete!");
}
```  

Add a `routeNotificationForMobizon` method to your Notifiable model to return the phone number:  

```php
public function routeNotificationForMobizon()
{
    //Phone Number without symbols or spaces
    return $this->phone_number;
}
```    

### Available methods

* `content()` - (string), SMS notification body

## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Testing

``` bash
$ composer test
```

## Security

If you discover any security related issues, please email sanzhar@aketai.com instead of using the issue tracker.

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

## Credits

- [Laraketai](https://github.com/laraketai)
- [All Contributors](../../contributors)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
