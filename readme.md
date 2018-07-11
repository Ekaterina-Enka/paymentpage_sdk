# ECommPay PHP SDK

[![Build Status](https://travis-ci.org/ITECOMMPAY/paymentpage_sdk.svg?branch=master)](https://travis-ci.org/ITECOMMPAY/paymentpage_sdk)
[![Test Coverage](https://api.codeclimate.com/v1/badges/13f0385331642461cba7/test_coverage)](https://codeclimate.com/github/ITECOMMPAY/paymentpage_sdk/test_coverage)
[![Maintainability](https://api.codeclimate.com/v1/badges/13f0385331642461cba7/maintainability)](https://codeclimate.com/github/ITECOMMPAY/paymentpage_sdk/maintainability)

This is a set of libraries in the PHP language to ease integration of your service
with the ECommPay Payment Page.

The following functionality is implemented:

* [x] Payment Page opening (URL only)
* [x] Callback handling

Note that for correct SDK operating your must run on PHP 7.0 or higher.  

## Payment flow

![Payment flow](flow.png)

## Installation

Install with composer

```bash
composer require ecommpay/paymentpage-sdk
```

### Get URL for payment

Specify the configuration settings (project ID, secret key) and the payment parameters. 

```php
$gate = new ecommpay\Gate('secret'); // Specify the secret key of your project
$payment = new ecommpay\Payment(100); // Specify the ID of your project
$payment->setPaymentAmount(1000)->setPaymentCurrency('EUR'); // Specify parameters for a payment  
$url = $gate->getPurchasePaymentPageUrl($payment); // Get the resulting URL
``` 

`$url` here is the signed URL that can be used to open payment widget in a browser tab.

### Handle callback from ECommPay

You'll need to autoload this code in order to handle callbacks:

```php
$gate = new ecommpay\Gate('secret'); 
$callback = $gate->handleCallback($data); 
```

* `$data` is the JSON data received from payment system.
* `$callback` is the Callback object describing properties received from payment system.

`$callback` implements the following methods: 

* `Callback::getPaymentStatus();` // Get payment status.
* `Callback::getPayment();` // Get all payment data.
* `Callback::getPaymentId();` // Get payment ID in your system.

## Update

Update with composer

```bash
composer update ecommpay/paymentpage-sdk
```

## Additional data

You can find additional information, such as payment statuses, request and callback parameters, in [https://developers.ecommpay.com/en/en_PP_API.html](Payment Page API). 

