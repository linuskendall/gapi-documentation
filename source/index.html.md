---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - python--boto2: boto2 (py)
  - python--boto3: boto3 (py)
  - ruby: Ruby 
  - php: PHP (SDK)
  - php--raw: PHP (no SDK)

toc_footers:
  - <a href='https://manage.thegcloud.com/index.php?act=api'>Get an API Key</a>
  - <a href='https://manage.thegcloud.com/'>GigeNET control panel</a>

includes:
  - authentication
  - api 
  - instance_types
  - types
  - errors

search: true
---

# Introduction

Welcome to the GigeNET API version 2. This API is more secure, provides greater flexibility as well as compatibility with a large range of tools and SDKs. We recommend that all new integrations are built using this API.

This API version has been designed to be compatible to as large degree as possible with the Amazon Webservices API focusing primarily on the so-called [Elastic Compute Cloud API](https://docs.aws.amazon.com/AWSEC2/latest/APIReference/Welcome.html). Compatibility with this API means that you can use the many different SDK available for different languages to interface with GigeNET's API just as you would Amazon web services. Some tools written for AWS might work without modification for use with our API, while others might require minimal changes. In addition to that, you can of course also set-up requests and connections directly to our API by easily implementing the interface yourself.

This guide is meant for you to aquaint yourself with the subset of the AWS API that we implement. You can also reference with the [AWS API](https://docs.aws.amazon.com/AWSEC2/latest/APIReference/Welcome.html) for more details, though beware that our API might ignore certain parameters specified in the AWS API documentation if they are incompatible or have no meaning with regards to our infrastructure.

## Overview of API

For each API request you construct a query string which is then cryptographically signed using your authentication details. The API will process your request and then either return an error, a return of value or data set based on your API action. You can provide arguments to the API either as part of the query string or via parameters sent as part of the request body.

Return values are returned as an XML document, containing the specified return values for each API function. If you need more examples of how the return values might look you can always also refer to the [AWS API documentation](https://docs.aws.amazon.com/AWSEC2/latest/APIReference/Welcome.html) for the corresponding API function call.

In case of errors, you will receive an HTTP error return code (400, 401 or 500) along with an XML document describing the error. 

The GigeNET API server URL is [https://api.thegcloud.com](https://api.thegcloud.com). All API actions should be sent to the API server URL.

## Supported AWS SDKs

All standard AWS SDKs should work with the API. Compatibility has been verified for the following:

 * AWS PHP SDK
 * AWS Ruby SDK
 * boto2 (Python)
 * boto3 (Python)

Other SDKs can be found on [the AWS pages](https://aws.amazon.com/tools/)..

## Installing the SDK

```python--boto2
# Install pip if required
easy_install pip

# Install the boto2 SDK
pip install boto
```

```python--boto3
# Install pip if required
easy_install pip

# Install the boto2 SDK
pip install boto3
```

```php
# Install composer
curl -sS https://getcomposer.org/installer | php

# Install the latest AWS SDK
php composer.phar require aws/aws-sdk-php
```

```ruby
# Install the latest AWS SDK
gem install aws-sdk
```

The SDKs can be installed using the standard package managers for your chosen languages.

Even though using one of these SDKs is the simplest way to access the API, you can also manually use the REST API using custom code to create integrations without an SDK. In this documentation we have provied some examples of how to authenticate and make API calls without using an SDK.

## Creating API tokens

Before you can use the API, you will need to enable it,  create a new API applications and generate API keys which you will then be using to authenticate with the API. You can access the API settings rom the [GigeNET client dashboard](http://manage.thegcloud.com/index.php?act=api).

### Step 1. Create a new API application in the GigeNET client dashboard.

![Create an application](1_step_new_app.gif "Creating a new application")

<aside class="notice">
An application is the website or application that will be exchanging data with the API server.
You must give your new application a name and specify the IP address of the server it will be running from.
Although it is required to add an API application to enable your settings, you will only be needing your API Key and Hash to establish authentication.
</aside>

![Updating application details](1_step_new_app_details.gif "Updating application details.")


### Step 2. Enable the use of the GigeNET API in your API settings.

![Enabling the API](2_step_enable_api.gif "Enabling the API.")

<aside class="notice">
The API is not enabled by default. Click the "Enable API" button and confirm in the pop up box.
</aside>

### Step 3. Now click "Update API Key and Hash" to obtain your API key and hash code.

![Update API token and hash](2_step_create_key.gif "Updating the API token and hash.")

<aside class="notice">
You should now have a API Key and API Hash.
These will allow you to connect to your VMs through the API so make sure you keep this info safe.
You can update your key and hash at any time however you will need to also update these settings in your web app.
</aside>

![You know have full access to the API.](2_step_success.gif "Success API tokens generated")


## Connecting to the API

```python--boto2
import boto

conn = boto.connect_ec2_endpoint(
	'https://api.thegcloud.com', 
	'APIKEY', 
	'APIHASH')
```

```python--boto3
import boto3

conn = boto3.client('ec2', 
		endpoint_url='https://api.thegcloud.com', 
		aws_access_key_id='APIKEY', 
		aws_secret_access_key='APIHASH', 
		region_name='ord1');
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;

$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));
```

```php--raw
<?php
/** 
* This example illustrates how to generate a signed URL to make an API request
* without depending on any external libraries.
*/

/**
* Generates an API signature for a given request using the V2 signature method.
*/
function signV2($method, $host, $uri, $qs, $signature_method, $secret_key) {
  $canonicalRequest = "$method\n$host\n$uri\n$qs";
  $signature_algos = 
		array('HmacSHA256' => 'sha256', 'HmacSHA1' => 'sha1' );

  return base64_encode(
    hash_hmac($signature_algos[$signature_method],
    $canonicalRequest,
    $secret_key,
    true));
}
/**
 * Constructs an API request URL
 */
function apiRequestURL($endpoint, $access_key, $secret_key, $Action, $Parameters) {
  $timestamp = new DateTime();
  $api_endpoint = parse_url($endpoint);

  if(!isset($api_endpoint['host']))
    throw new Exception('Invalid endpoint URL provided');
  if(!isset($api_endpoint['scheme']))
    $api_endpoint['scheme'] = 'http';
  if(!isset($api_endpoint['path']))
    $api_endpoint['path'] = '/';

  $qs = 'AWSKeyId='.$access_key
    .'&Action='.$Action
    .'&SignatureMethod=HmacSHA256'
    .'&SignatureVersion=2'
    .'&Timestamp='.urlencode($timestamp->format("c"))
    .$Parameters;

  return $api_endpoint['scheme'].'://'.$api_endpoint['host'].'?'.$qs
    .'&Signature='.urlencode(
      signV2('GET',
          $api_endpoint['host'],
          $api_endpoint['path'],
          $qs,
          'HmacSHA256',
          $secret_key));
}

$api_url = 'https://api.thegcloud.com';
$access_key = 'APIKEY';
$secret_key = 'APIHASH';

$url = apiRequestUrl($api_url, $access_key, $secret_key, 'APIACTION', '&Param1=Val&Param2=Val');

// $url can now be fetched using GET HTTP Request
```


```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Resource.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
```

> Make sure to replace `APIKEY` with your API key and `APIHASH` with your API hash from the API settings page.

Once you have an API key and hash you can use them together with the SDK of your choice, or generated signed requests through your own code. Sample code for connecting to the API is available on the left.


