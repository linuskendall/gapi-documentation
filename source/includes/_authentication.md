# Authentication

All requests to the API are required to be cryptographically signed. By first generating the request parameters and then applying a cryptographic hash function to the request before you send it you prove that the request really originated from you. In this way, we can verify the request but we can also ensure that expired requests are not re-used in case somebody gets access to the request.

The signed requests are authenticated without transferring any secrets over the network, this means that while we recommend you always use HTTPS to ensure an SSL/TLS encrypted connection to the API, the request URLs themselves are not secret. The API hash/secret key should never be transferred over the network and should remain with you locally. Each request also has a timestamp or an expiry date affixed to it, meaning that if you want you can pre-create and pre-sign requests for a later date. Remember though that a signed request will be accepted by our servers as originating from you  - if you pre-create signed URLs and subsequently loose control of them you will need to reset the API token.

We support the same process of signing requests as the Amazon Web Services API with both the V2 and V4 signing process supported. This means that you can follow their guide with regards to how to sign requests: http://docs.aws.amazon.com/general/latest/gr/signing_aws_api_requests.html.

You can also generate new time limited secrets and access tokens using the GetSessionToken API call (described below). This is useful if you want to generate temporary credentials which can be used in exactly the same way as normal credentials. If you are using a temporary session token, you will need to attach it to every request as described in the [AWS API documentation](http://docs.aws.amazon.com/STS/latest/UsingSTS/using-temp-creds.html).

## Signing schemes

You can use either the AWS [V2](https://docs.aws.amazon.com/general/latest/gr/signature-version-2.html) or [V4](https://docs.aws.amazon.com/general/latest/gr/signature-version-4.html) signing process to send requests to our API. The V2 process generates a signature and appends it as a query string parameter, while the V4 process uses an `Authorization` header. The V4 process is the recommended one and is the one that all SDKs support. 

Sample V2 signed request URL:

`https://api.thegcloud.com?&AWSAccessKeyId=APIKEY&Action=DescribeInstances&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2011-10-03T15%3A19%3A30&Version=2009-03-31&Signature=calculated value`

Sample V4 Authorization header:

`Authorization: AWS4-HMAC-SHA256 Credential=APIKEY/20180304/ord1/ec2/aws4_request, SignedHeaders=content-type;host;x-amz-content-sha256;x-amz-date, Signature=calculated value`

In the AWS API documentation you can find extensive details on how to generate a [V2 signature](https://docs.aws.amazon.com/general/latest/gr/signature-version-2.html) or a [V4 signature](https://docs.aws.amazon.com/general/latest/gr/signature-version-4.html).

<aside class="notice">
You use your <code>APIHASH</code> to generate the signature, but this should never be provided in clear text in any of the API calls or transmitted over the wire. 
</aside>

## Session Tokens

```python--boto2
import boto
import boto.sts
from boto.regioninfo import RegionInfo

sts = boto.sts.STSConnection(aws_access_key_id='APIKEY',
                             aws_secret_access_key='APIHASH',
                             is_secure=True,
                             path='/'
                             region=RegionInfo(name='ord1', 
				                      endpoint='api.thegcloud.com'))

session = sts.get_session_token()
```

```python--boto3
import boto3

sts = boto3.client('sts',
        endpoint_url='https://api.thegcloud.com',
        aws_access_key_id='APIKEY',
        aws_secret_access_key='APIHASH',
        region_name='ord1');

session = sts.get_session_token()
```

```ruby
require 'aws-sdk'

sts = Aws::STS::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH',
  http_wire_trace: true
)

session = sts.get_session_token()
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Sts\StsClient;

$stsClient = StsClient::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$session = $stsClient->GetSessionToken();
```

```php--raw
<?php
/** 
* This example uses Guzzle which can be installed through composer: php composer.phar require guzzle/guzzle
*/
require('vendor/autoload.php');

Guzzle\Http\StaticClient::mount();

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
    .'&Timestamp='.urlencode($timestamp->format("c"));

  if(is_array($Parameters)) {
    foreach($params as $key => $value) {
      $qs .= "&".$key."=".urlencode($value);
    }
  } else {
    if(substr($Parameters, 0, 1) !== '&') $qs .= '&';
    $qs .= $Parameters;
  }

  return $api_endpoint['scheme'].'://'.$api_endpoint['host'].'?'.$qs
    .'&Signature='.urlencode(
      signV2('GET',
          $api_endpoint['host'],
          $api_endpoint['path'],
          $qs,
          'HmacSHA256',
          $secret_key));
}
/**
 * Executes an API request
 */
function apiRequest($Action, $Parameters='') {
  global $api_url, $access_key, $secret_key;
  $res = Guzzle::get(apiRequestUrl($api_url, $access_key, $secret_key, $Action, $Parameters));
  return $res->getBody();
}

$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

$sessionXml = apiRequest('GetSessionToken');
```

To get time limited session tokens, we provide a small subset of the [AWS STS API](https://docs.aws.amazon.com/STS/latest/APIReference/Welcome.html) to allow you to generate time limited tokens. This can be useful in the scenario where you want a trusted service to provide tokens to less trusted services or user applications. As these tokens are time limited, there is less risk of issuing and providing these than there is in providing your main API credentials. 

> The GetSessionToken API call returns XML like this:

```xml
<?xml version="1.0" encoding="utf-8"?>
<GetSessionTokenResponse>
  <GetSessionTokenResult>
    <Credentials>
      <SessionToken>SESSIONTOKEN</SessionToken>
      <SecretAccessKey>SECRETACCESSKEY</SecretAccessKey>
      <Expiration>2018-03-04T12:21:50+00:00</Expiration>
      <AccessKeyId>SESSIONACCESSKEY</AccessKeyId>
    </Credentials>
  </GetSessionTokenResult>
  <RequestID>12e6d6095ad5912a8b209e42e466afdb</RequestID>
</GetSessionTokenResponse>
```

### Parameters

Parameter | Default | Required | Description
--------- | ------- | -------- | -----------
DurationSeconds | 3600 | false | The number of seconds that the token should be valid for, minimum 900 and maximum 129600.
