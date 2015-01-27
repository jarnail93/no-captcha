No CAPTCHA reCAPTCHA [![Build Status](https://travis-ci.org/anhskohbo/no-captcha.svg?branch=master&style=flat-square)](https://travis-ci.org/anhskohbo/no-captcha)
==========

![recaptcha_anchor 2x](https://cloud.githubusercontent.com/assets/1529454/5291635/1c426412-7b88-11e4-8d16-46161a081ece.gif)

> For Laravel 5, please use `master` brand.

## Installation

Add the following line to the `require` section of `composer.json`:

```json
{
    "require": {
        "anhskohbo/no-captcha": "1.*"
    }
}
```

Run `composer update`.

## Laravel 4

### Setup

Add ServiceProvider to the providers array in `app/config/app.php`.

```
'Anhskohbo\NoCaptcha\NoCaptchaServiceProvider',
```

### Configuration

Run `php artisan config:publish anhskohbo/no-captcha`.

Fill secret and sitekey config in `app/config/packages/anhskohbo/no-captcha/config.php` file:

```php
<?php

return array(

	'secret'  => '',
	'sitekey' => '',

);
```

### Usage

##### Display reCAPTCHA

Insert reCAPTCHA inside your form using one of this examples:

```php
{{ Form::open() }}
	{{ Form::captcha() }}
	{{ Form::submit() }}
{{ Form::close() }}
```

##### Validation

Add `'g-recaptcha-response' => 'required|captcha'` to rules array.

```php

$validate = Validator::make(Input::all(), [
	'g-recaptcha-response' => 'required|captcha'
]);

```

## Without Laravel

Checkout example below:

```php
<?php

require_once "vendor/autoload.php";

use Anhskohbo\NoCaptcha\NoCaptcha;

$captcha = new NoCaptcha('[secret]', '[sitekey]');

if ( ! empty($_POST)) {
    var_dump($captcha->verifyResponse($_POST['g-recaptcha-response']));
    exit();
}

?>

<form action="?" method="POST">
    <?php echo $captcha->display(); ?>
    <button type="submit">Submit</button>
</form>

```

## Contribute

https://github.com/anhskohbo/no-captcha/pulls
