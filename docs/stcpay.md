# STCPAY

STC Pay is a mobile wallet used to pay your day to day expenses, it is a local payment option which is supported in KSA.\


To complete a payment, the customer can check out using the phone number , and the OTP is received as an SMS.

## Supported Channels

You can integrate STC Pay through the following options:\


**Redirection:** Means you will redirect your customer to a payment page hosted on the Amazon Payment Services to submit their payment details and completes the payment then redirects the customer to your website.\


**Merchant page:** For a smoother payment experience you can choose to integrate STC Pay checkout into your website. Means your customer will complete the payment inside your website without redirection( Integrating it directly into your checkout page).

## STCPAY And Tokenization

Tokenization is supported with the two channels "Redirection" , "Merchant Page".

By using Tokenization, your customer does not need to enter their phone number to proceed with checkout. Instead, your customer's phone number will be displayed in a masked format on the checkout screen.\
Its also removes the requirement to verify transactions with an OTP because using a token name with STC Pay implies a downgraded transaction.\


Tokenization work flow:\


**1-** The customer should complete the first payment through STCPAY successfully which will always be protected by requesting an OTP.\
as well activation the tokenization in the customer STC Pay app is mandatory.\


**2-** In the second payment for the customer , the saved phone number will be listed in the checkout page in order to proceed with the payment directly without submitting the OTP number.\


Please refer to the sections below for more technical details:\
[Redirection checkout flow using a token](broken-reference)\
[Merchant page integration checkout flow using a token](broken-reference)\


## Checkout Workflows

### Redirection checkout using a one-time PIN

When your customer is ready to pay, your website redirects your customer to the Amazon Payment Services payment page. Your customer completes their payment details on the Amazon Payment Services in a two-step process.

* First, your customer enters their phone number on the Amazon Payment Services payment page. That generates an STC Pay OTP code, which is sent to your customer via SMS.
* On the next screen, your customer enters the OTP to complete the payment. Your customer is then redirected back to your website.

### Redirection checkout flow using a token

**1-** For the first customer payment, You need to process the APi request STCPAY Redirection ,if the payment simulated successfully with submitting a proper customer OTP, as well the tokenization is active in the customer STC Pay app then we will return in the response an extra parameter called "token\_name".\
**2-** For the next customer payment ,Your customer simply needs to select their masked phone number to complete the transaction in a single step. You should include the token\_name received from the first checkout in your STCPAY Redirection.\


### Merchant page integration checkout flow using a one-time PIN

When you choose to build your own payment page and you do not use a token, you need to process a payment in two steps:

* **Generate OTP**: First, your server needs to send a request to the Amazon Payment Services server in order to generate an OTP for the customer. In this request you include your customer’s phone number. Amazon Payment Services generates an OTP based on this number. The OTP is sent to your customer’s mobile phone by SMS and your customer enters the OTP on your checkout page. The length of the OTP can be 4, 5 or 6 characters. During integration, update the OTP field to be dynamic, so it can accept any length.
* **Purchase**: Next, once the OTP is validated, you send a purchase request to Amazon Payment Services to complete the payment. You need to include the same merchant reference number that you use to request the OTP. The length of the OTP can be 4, 5 or 6 characters. During integration, update the OTP field to be dynamic, so it can accept any length.

### Merchant page integration checkout flow using a token

When you build your own payment page and your customer completes a payment using a token, you only need to build one step into your checkout process.

*   **Purchase**: Because the OTP has already been validated, you can simply send a purchase request to Amazon Payment Services to complete the payment. It enables your customer to complete their purchase while skipping the OTP process.

    **NOTE: You need to perform OTP workflow at least once to generate a token before you can process a payment without the OTP. The length of the OTP can be 4, 5 or 6 characters. During integration, update the OTP field to be dynamic, so it can accept any length.**

## STCPAY Redirection

### Redirection URLs

**Test Environment URL:**\
\
Test URL: https://sbcheckout.payfort.com/FortAPI/paymentPage\
\
**Production Environment URL:**\
\
Production URL: https://checkout.payfort.com/FortAPI/paymentPage\
\


### Parameters Submission Type

HTTPs Form Post Request.\


### Purchase - Request

**Include the following parameters in the request you will send to Amazon Payment Services:**

```shell
{
    {
    "amount": "68557",
    "digital_wallet": "STCPAY",
    "signature": "{{signature}}",
    "merchant_identifier": "{{merchant_identifier}}",
    "access_code": "FIX7skJDGmjJF0WDh2oB",
    "customer_ip": "127.0.0.1",
    "language": "en",
    "otp": "12345",
    "command": "PURCHASE",
    "merchant_reference": "merchantTest-10117",
    "customer_email": "merchant07@merchantdomain.com",
    "return_url": "http://127.0.0.1/merchantSHEK/payment/stcResponse",
    "currency": "SAR",
    "phone_number": "0551111111",
    "remember_me": "YES"
}
}
```

```php
error_reporting(E_ALL);
ini_set('display_errors', '1');

$url = 'https://sbpaymentservices.payfort.com/FortAPI/paymentApi';

$arrData = array(
    {
        'amount'=> '68557',
    'digital_wallet'=> 'STCPAY',
    'signature'=> '{{signature}}',
    'merchant_identifier'=> '{{merchant_identifier}}',
    'access_code'=> 'FIX7skJDGmjJF0WDh2oB',
    'customer_ip'=> '127.0.0.1',
    'language'=> 'en',
    'otp'=> '12345',
    'command'=> 'PURCHASE',
    'merchant_reference'=> 'merchantTest-10117',
    'customer_email'=> 'merchant07@merchantdomain.com',
    'return_url'=> 'http://127.0.0.1/merchantSHEK/payment/stcResponse',
    'currency'=> 'SAR',
    'phone_number'=> '0551111111',
    'remember_me'=> 'YES'
}

   
);


$ch = curl_init( $url );
# Setup request to send json via POST.
$data = json_encode($arrData);
curl_setopt( $ch, CURLOPT_POSTFIELDS, $data );
curl_setopt( $ch, CURLOPT_HTTPHEADER, array('Content-Type:application/json'));
# Return response instead of printing.
curl_setopt( $ch, CURLOPT_RETURNTRANSFER, true );
# Send request.
$result = curl_exec($ch);
curl_close($ch);
# Print response.
echo "<pre>$result</pre>";
```

```python
import urllib
import urllib2
import json

url = 'https://sbpaymentservices.payfort.com/FortAPI/paymentApi';

arrData = 
    {
        'amount: '68557',
    'digital_wallet: 'STCPAY',
    'signature: '{{signature}}',
    'merchant_identifier: '{{merchant_identifier}}',
    'access_code: 'FIX7skJDGmjJF0WDh2oB',
    'customer_ip: '127.0.0.1',
    'language: 'en',
    'otp: '12345',
    'command: 'PURCHASE',
    'merchant_reference: 'merchantTest-10117',
    'customer_email: 'merchant07@merchantdomain.com',
    'return_url: 'http://127.0.0.1/merchantSHEK/payment/stcResponse',
    'currency: 'SAR',
    'phone_number: '0551111111',
    'remember_me: 'YES'

    
};


values = json.dumps(arrData)
data = urllib.urlencode(values)
req = urllib2.Request(url, data)
response = urllib2.urlopen(req)
page = response.read()
print page + '\n\n'
```

```ruby
require 'json'
require 'net/http'
require 'net/https'
require 'uri'
require 'openssl'
arrData = 

    {
        'amount'=> '68557',
    'digital_wallet'=> 'STCPAY',
    'signature'=> '{{signature}}',
    'merchant_identifier'=> '{{merchant_identifier}}',
    'access_code'=> 'FIX7skJDGmjJF0WDh2oB',
    'customer_ip'=> '127.0.0.1',
    'language'=> 'en',
    'otp'=> '12345',
    'command'=> 'PURCHASE',
    'merchant_reference'=> 'merchantTest-10117',
    'customer_email'=> 'merchant07@merchantdomain.com',
    'return_url'=> 'http://127.0.0.1/merchantSHEK/payment/stcResponse',
    'currency'=> 'SAR',
    'phone_number'=> '0551111111',
    'remember_me'=> 'YES'
}
;
arrData.each {|key, value|
  puts key +value ;
}

arrData = arrData.to_json
uri = URI.parse("https://sbpaymentservices.payfort.com/FortAPI/paymentApi")
http = Net::HTTP.new(uri.host, uri.port)
http.use_ssl = true
http.verify_mode = OpenSSL::SSL::VERIFY_NONE
request = Net::HTTP::Post.new("/v1.1/auth")
request.add_field('Content-Type', 'application/json')
request.body = arrData
response = http.request(request)
```

```java
String jsonRequestString = "{\n    \"amount\": \"68557\",\n    \"digital_wallet\": \"STCPAY\",\n    \"signature\": \"\",\n    \"merchant_identifier\": \"{{merchant_identifier}}\",\n    \"access_code\": \"FIX7skJDGmjJF0WDh2oB\",\n    \"customer_ip\": \"127.0.0.1\",\n    \"language\": \"en\",\n    \"otp\": \"12345\",\n    \"command\": \"PURCHASE\",\n    \"merchant_reference\": \"merchantTest-10117\",\n    \"customer_email\": \"merchant07@merchantdomain.com\",\n    \"return_url\": \"http://127.0.0.1/merchantSHEK/payment/stcResponse\",\n    \"currency\": \"SAR\",\n    \"phone_number\": \"0551111111\",\n    \"remember_me\": \"YES\"\n}";

// Define and Initialize HttpClient
HttpClient httpClient = HttpClientBuilder.create().build();
// Intialize HttpPOST with FORT Payment services URL
HttpPost request = new HttpPost("https://sbpaymentservices.payfort.com/FortAPI/paymentApi");
// Setup Http POST entity with JSON String
StringEntity params = new StringEntity(jsonRequestString);
// Setup request type as JSON
request.addHeader("content-type", "application/json");
request.setEntity(params);
// Post request to FORT
HttpResponse response = httpClient.execute(request);
// Read response using StringBuilder
StringBuilder sb = new StringBuilder();
BufferedReader reader = new BufferedReader(new InputStreamReader(
  response.getEntity().getContent()), 65728);
String line = null;
while ((line = reader.readLine()) != null) {
sb.append(line);
}
// Print response
System.out.println(sb.toString());
```

| ATTRIBUTES                                                                          | Description                                                                                                                                                                                                                               |
| ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>command</strong><br>Alpha<br>Mandatory<br>Max: 20</p>                    | <p>A command.<br>Possible/ expected values: PURCHASE</p>                                                                                                                                                                                  |
| <p><strong>access_code</strong><br>Alphanumeric<br>Mandatory<br>Max: 20</p>         | <p>Access code.<br>Example: zx0IPmPy5jp1vAz8Kpg7</p>                                                                                                                                                                                      |
| <p><strong>digital_wallet</strong><br>Alpha<br>Mandatory<br>Max: 20</p>             | <p>Digital wallet used for transaction.<br>Possible/ expected values: STCPAY</p>                                                                                                                                                          |
| <p><strong>merchant_identifier</strong><br>Alphanumeric<br>Mandatory<br>Max: 20</p> | <p>The ID of the Merchant.<br>Example: CycHZxVj</p>                                                                                                                                                                                       |
| <p><strong>merchant_reference</strong><br>Alphanumeric<br>Mandatory<br>Max: 40</p>  | <p>The Merchant’s unique order number.<br>Example: XYZ9239-yu898<br>Special characters: - _ .</p>                                                                                                                                         |
| <p><strong>amount</strong><br>Numeric<br>Mandatory<br>Max: 10</p>                   | <p>The transaction's amount. *Each currency has predefined allowed decimal points that should be taken into consideration when sending the amount check the note after this table.<br>Example: 10000</p>                                  |
| <p><strong>currency</strong><br>Alpha<br>Mandatory<br>Max: 3</p>                    | <p>The currency of the transaction’s amount in ISO code 3.<br>Possible/ expected values: SAR</p>                                                                                                                                          |
| <p><strong>token_name</strong><br>Alphanumeric<br>Optional<br>Max: 100</p>          | <p>The Token received from the Tokenization process.<br>Example: Op9Vmp<br>Special characters: . @ - _</p>                                                                                                                                |
| <p><strong>language</strong><br>Alpha<br>Mandatory<br>Max: 2</p>                    | <p>The checkout page and messages language.<br>Possible/ expected values: en/ ar</p>                                                                                                                                                      |
| <p><strong>customer_email</strong><br>Alphanumeric<br>Mandatory<br>Max: 254</p>     | <p>The customer's email.<br>Example: customer1@domain.com<br>Special characters: _ - . @ +</p>                                                                                                                                            |
| <p><strong>customer_ip</strong><br>Alphanumeric<br>Optional<br>max: 45</p>          | <p>It holds the customer's IP address. *We support IPv4 and IPv6 as shown in the example below.<br>Example:<br>IPv4 → 192.178.1.10<br>IPv6 → 2001:0db8:3042:0002:5a55:caff:fef6:bdbf<br>Special characters: . :</p>                       |
| <p><strong>signature</strong><br>Alphanumeric<br>Mandatory<br>Max: 200</p>          | <p>A string hashed using the Secure Hash Algorithm. Please refer to section <a href="broken-reference">Signature</a><br>Example: 7cad05f0212ed933c9a5d5dffa31661acf2c827a</p>                                                             |
| <p><strong>order_description</strong><br>Alphanumeric<br>Optional<br>Max: 150</p>   | <p>It holds the description of the order.<br>Example: iPhone 6-S<br>Special characters: <code>'</code> / . _ - # : $ <strong>Space</strong></p>                                                                                           |
| <p><strong>customer_name</strong><br>Alpha<br>Optional<br>Max: 40</p>               | <p>The customer's name.<br>Example: John Smith<br>Special characters: _ \ / - . <code>'</code> <strong>Space</strong></p>                                                                                                                 |
| <p><strong>merchant_extra</strong><br>Alphanumeric<br>Optional<br>Max: 999</p>      | <p>Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.<br>Example: JohnSmith<br>Special characters: . ; / _ - , <code>'</code> @</p>                                            |
| <p><strong>merchant_extra1</strong><br>Alphanumeric<br>Optional<br>Max: 250</p>     | <p>Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.<br>Example: JohnSmith<br>Special characters: . ; / _ - , <code>'</code> @</p>                                            |
| <p><strong>merchant_extra2</strong><br>Alphanumeric<br>Optional<br>Max: 250</p>     | <p>Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.<br>Example: JohnSmith<br>Special characters: . ; / _ - , <code>'</code> @</p>                                            |
| <p><strong>merchant_extra3</strong><br>Alphanumeric<br>Optional<br>Max: 250</p>     | <p>Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.<br>Example: JohnSmith<br>Special characters: . ; / _ - , <code>'</code> @</p>                                            |
| <p><strong>merchant_extra4</strong><br>Alphanumeric<br>Optional<br>Max: 250</p>     | <p>Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.<br>Example: JohnSmith<br>Special characters: . ; / _ - , <code>'</code> @</p>                                            |
| <p><strong>remember_me</strong><br>Alpha<br>Optional<br>Max: 2</p>                  | <p>This parameter provides you with an indication to whether to save this token for the user based on the user selection.<br>Possible/ expected values: -YES -NO</p>                                                                      |
| <p><strong>payment_option</strong><br>Alpha<br>Optional<br>Max: 10</p>              | <p>Payment option.<br>Possible/ expected values: STCPAY<br></p>                                                                                                                                                                           |
| <p><strong>phone_number</strong><br>Alphanumeric<br>Optional<br>max: 19</p>         | The customer's phone number.                                                                                                                                                                                                              |
| <p><strong>settlement_reference</strong><br>Alphanumeric<br>Optional<br>max: 34</p> | <p>The Merchant submits unique value to Amazon Payment Services. The value is then passed to the Acquiring bank and displayed to the merchant in the Acquirer settlement file.<br>Example: XYZ9239-yu898<br>Special characters: - _ .</p> |
| <p><strong>return_url</strong><br>Alphanumeric<br>Optional<br>Max: 400</p>          | <p>The URL of the Merchant's page that will be displayed to the customer when the order is processed.<br>Example: https://www.merchant.com<br>Special characters: $ ! = ? # &#x26; - _ / : .</p>                                          |

### Redirection - Response

**The following parameters will be returned in PayFort's Response:**

| ATTRIBUTES                                                              | Description                                                                                                                                                                                                                                                                                  |
| ----------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>command</strong><br>Alpha<br>Max: 20</p>                     | <p>A command.<br>Possible/ expected values: PURCHASE</p>                                                                                                                                                                                                                                     |
| <p><strong>response_code</strong><br>Numeric<br>Max: 5</p>              | <p>Response Code carries the value of our system's response. *The code consists of five digits, the first 2 digits represent the response <a href="broken-reference">status</a>, and the last 3 digits represent the response <a href="broken-reference">messages</a>.<br>Example: 20064</p> |
| <p><strong>response_message</strong><br>Alphanumeric<br>Max: 150</p>    | <p>The message description of the response code; it returns according to the request language.<br>Possible/ expected values: Please refer to section <a href="broken-reference">messages</a></p>                                                                                             |
| <p><strong>access_code</strong><br>Alphanumeric<br>Max: 20</p>          | <p>Access code.<br>Example: zx0IPmPy5jp1vAz8Kpg7</p>                                                                                                                                                                                                                                         |
| <p><strong>digital_wallet</strong><br>Alpha<br>Max: 20</p>              | <p>Digital wallet used for transaction.<br>Possible/ expected values: STCPAY</p>                                                                                                                                                                                                             |
| <p><strong>merchant_identifier</strong><br>Alphanumeric<br>Max: 20</p>  | <p>The ID of the Merchant.<br>Example: CycHZxVj</p>                                                                                                                                                                                                                                          |
| <p><strong>merchant_reference</strong><br>Alphanumeric<br>Max: 40</p>   | <p>The Merchant’s unique order number.<br>Example: XYZ9239-yu898</p>                                                                                                                                                                                                                         |
| <p><strong>amount</strong><br>Numeric<br>Max: 10</p>                    | <p>The transaction's amount.<br>Example: 10000</p>                                                                                                                                                                                                                                           |
| <p><strong>currency</strong><br>Alpha<br>Max: 3</p>                     | <p>The currency of the transaction’s amount in ISO code 3.<br>Possible/ expected values: SAR</p>                                                                                                                                                                                             |
| <p><strong>language</strong><br>Alpha<br>Max: 2</p>                     | <p>The checkout page and messages language.<br>Possible/ expected values: en/ ar</p>                                                                                                                                                                                                         |
| <p><strong>customer_email</strong><br>Alphanumeric<br>Max: 254</p>      | <p>The customer's email.<br>Example: customer1@domain.com</p>                                                                                                                                                                                                                                |
| <p><strong>customer_ip</strong><br>Alphanumeric<br>max: 45</p>          | <p>It holds the customer's IP address. *We support IPv4 and IPv6 as shown in the example below.<br>Example:<br>IPv4 → 192.178.1.10<br>IPv6 → 2001:0db8:3042:0002:5a55:caff:fef6:bdbf</p>                                                                                                     |
| <p><strong>signature</strong><br>Alphanumeric<br>Max: 200</p>           | <p>A string hashed using the Secure Hash Algorithm. Please refer to section <a href="broken-reference">Signature</a><br>Example: 7cad05f0212ed933c9a5d5dffa31661acf2c827a</p>                                                                                                                |
| <p><strong>eci</strong><br>Alpha<br>Max: 16</p>                         | <p>Ecommerce indicator.<br>Possible/ expected values: ECOMMERCE</p>                                                                                                                                                                                                                          |
| <p><strong>payment_option</strong><br>Alpha<br>Max: 10</p>              | <p>Payment option.<br>Possible/ expected values: STCPAY<br></p>                                                                                                                                                                                                                              |
| <p><strong>fort_id</strong><br>Numeric<br>Max: 20</p>                   | <p>The order's unique reference returned by our system.<br>Example: 149295435400084008</p>                                                                                                                                                                                                   |
| <p><strong>status</strong><br>Numeric<br>Max: 2</p>                     | <p>A two-digit numeric value that indicates the status of the transaction.<br>Possible/ expected values: Please refer to section <a href="broken-reference">statuses</a></p>                                                                                                                 |
| <p><strong>token_name</strong><br>Alphanumeric<br>max: 100</p>          | <p>The Token received from the Tokenization process.<br>Example: COp9Vmp</p>                                                                                                                                                                                                                 |
| <p><strong>order_description</strong><br>Alphanumeric<br>Max: 150</p>   | <p>A description of the order.<br>Example: iPhone 6-S</p>                                                                                                                                                                                                                                    |
| <p><strong>customer_name</strong><br>Alpha<br>Max: 40</p>               | <p>The customer's name.<br>Example: John Smith</p>                                                                                                                                                                                                                                           |
| <p><strong>merchant_extra</strong><br>Alphanumeric<br>Max: 999</p>      | <p>Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.<br>Example: JohnSmith</p>                                                                                                                                                   |
| <p><strong>merchant_extra1</strong><br>Alphanumeric<br>Max: 250</p>     | <p>Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.<br>Example: JohnSmith</p>                                                                                                                                                   |
| <p><strong>merchant_extra2</strong><br>Alphanumeric<br>Max: 250</p>     | <p>Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.<br>Example: JohnSmith</p>                                                                                                                                                   |
| <p><strong>merchant_extra3</strong><br>Alphanumeric<br>Max: 250</p>     | <p>Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.<br>Example: JohnSmith</p>                                                                                                                                                   |
| <p><strong>merchant_extra4</strong><br>Alphanumeric<br>Max: 250</p>     | <p>Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.<br>Example: JohnSmith</p>                                                                                                                                                   |
| <p><strong>remember_me</strong><br>Alpha<br>Max: 3</p>                  | <p>This parameter provides you with an indication to whether to save this token for the user based on the user selection.<br>Possible/ expected values: -YES -NO</p>                                                                                                                         |
| <p><strong>phone_number</strong><br>Alphanumeric<br>max: 19</p>         | The customer's phone number. It will be returned if it is shared in request.                                                                                                                                                                                                                 |
| <p><strong>settlement_reference</strong><br>Alphanumeric<br>max: 34</p> | <p>The Merchant submits unique value to Amazon Payment Services. The value is then passed to the Acquiring bank and displayed to the merchant in the Acquirer settlement file.<br>Example: XYZ9239-yu898</p>                                                                                 |

## STCPAY Merchant Page

### Generate OTP URLs

**Test Environment URL:**\
\
Test URL: https://sbpaymentservices.payfort.com/FortAPI/paymentApi\
\
**Production Environment URL:**\
\
Production URL: https://paymentservices.payfort.com/FortAPI/paymentApi\
\


### Parameters Submission Type

REST POST request using JSON.\


### Generate OTP - Request

**Include the following parameters in the request you will send to Amazon Payment Services:**

```shell
{
    "amount": "68557",
    "service_command": "GENERATE_OTP",
    "digital_wallet": "STCPAY",
    "signature": "{{signature}}",
    "merchant_identifier": "{{merchant_identifier}}",
    "merchant_reference": "merchantTest-10090",
    "access_code": "{{access_code}}",
    "currency": "SAR",
    "language": "en",
    "phone_number": "0551111111"
}
```

```php
error_reporting(E_ALL);
ini_set('display_errors', '1');

$url = 'https://sbpaymentservices.payfort.com/FortAPI/paymentApi';
$arrData = array(
    {
    'amount'=> '68557',
    'service_command'=> 'GENERATE_OTP',
    'digital_wallet'=> 'STCPAY',
    'signature'=> '{{signature}}',
    'merchant_identifier'=> '{{merchant_identifier}}',
    'merchant_reference'=> 'merchantTest-10090',
    'access_code'=> '{{access_code}}',
    'currency'=> 'SAR',
    'language'=> 'en',
    'phone_number'=> '0551111111'
}

   
);


$ch = curl_init( $url );
# Setup request to send json via POST.
$data = json_encode($arrData);
curl_setopt( $ch, CURLOPT_POSTFIELDS, $data );
curl_setopt( $ch, CURLOPT_HTTPHEADER, array('Content-Type:application/json'));
# Return response instead of printing.
curl_setopt( $ch, CURLOPT_RETURNTRANSFER, true );
# Send request.
$result = curl_exec($ch);
curl_close($ch);
# Print response.
echo "<pre>$result</pre>";
```

```python
import urllib
import urllib2
import json
url = 'https://sbpaymentservices.payfort.com/FortAPI/paymentApi';

arrData = {
    
        'amount': '68557',
    'service_command': 'GENERATE_OTP',
    'digital_wallet': 'STCPAY',
    'signature': '{{signature}}',
    'merchant_identifier': '{{merchant_identifier}}',
    'merchant_reference': 'merchantTest-10090',
    'access_code': '{{access_code}}',
    'currency': 'SAR',
    'language': 'en',
    'phone_number': '0551111111'

    
};


values = json.dumps(arrData)
data = urllib.urlencode(values)
req = urllib2.Request(url, data)
response = urllib2.urlopen(req)
page = response.read()
print page + '\n\n'
```

```ruby
require 'json'
require 'net/http'
require 'net/https'
require 'uri'
require 'openssl'
arrData = 

    {
        'amount'=> '68557',
    'service_command'=> 'GENERATE_OTP',
    'digital_wallet'=> 'STCPAY',
    'signature'=> '{{signature}}',
    'merchant_identifier'=> '{{merchant_identifier}}',
    'merchant_reference'=> 'merchantTest-10090',
    'access_code'=> '{{access_code}}',
    'currency'=> 'SAR',
    'language'=> 'en',
    'phone_number'=> '0551111111'
}
;
arrData = arrData.to_json
uri = URI.parse("https://sbpaymentservices.payfort.com/FortAPI/paymentApi")
http = Net::HTTP.new(uri.host, uri.port)
http.use_ssl = true
http.verify_mode = OpenSSL::SSL::VERIFY_NONE
request = Net::HTTP::Post.new("/v1.1/auth")
request.add_field('Content-Type', 'application/json')
request.body = arrData
response = http.request(request)
```

```java
String jsonRequestString = "{\n    \"service_command\": \"GENERATE_OTP\",\n    \"access_code\": \"{{access_code}}\",\n    \"merchant_identifier\": \"{{merchant_identifier}}\",\n    \"merchant_reference\": \"AbhiTest-10080\",\n    \"amount\": \"125000\",\n    \"currency\": \"AED\",\n    \"language\": \"en\",\n    \"customer_email\": \"abhivit@amazon.com\",\n    \"request_expiry_date\":\"2022-07-22T15:36:55+03:00\",\n    \"notification_type\":\"EMAIL\",\n    \"signature\": \"fb466699104651adb8c3eace5a3d8ea8e2dbd4739330b7379a6ece4956bed14b\"\n}";

// Define and Initialize HttpClient
HttpClient httpClient = HttpClientBuilder.create().build();
// Intialize HttpPOST with FORT Payment services URL
HttpPost request = new HttpPost("https://sbpaymentservices.payfort.com/FortAPI/paymentApi");
// Setup Http POST entity with JSON String
StringEntity params = new StringEntity(jsonRequestString);
// Setup request type as JSON
request.addHeader("content-type", "application/json");
request.setEntity(params);
// Post request to FORT
HttpResponse response = httpClient.execute(request);
// Read response using StringBuilder
StringBuilder sb = new StringBuilder();
BufferedReader reader = new BufferedReader(new InputStreamReader(
  response.getEntity().getContent()), 65728);
String line = null;
while ((line = reader.readLine()) != null) {
sb.append(line);
}
// Print response
System.out.println(sb.toString());
```

| ATTRIBUTES                                                                          | Description                                                                                                                                                                                                                                                                            |
| ----------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>service_command</strong><br>Alpha<br>Mandatory<br>Max: 20</p>            | <p>Command.<br>Possible/ expected values: GENERATE_OTP</p>                                                                                                                                                                                                                             |
| <p><strong>access_code</strong><br>Alphanumeric<br>Mandatory<br>Max: 20</p>         | <p>Access code.<br>Example: zx0IPmPy5jp1vAz8Kpg7</p>                                                                                                                                                                                                                                   |
| <p><strong>amount</strong><br>Numeric<br>Mandatory<br>Max: 10</p>                   | <p>The transaction amount to generate the OTP, this amount must also be used for the purchase transaction. *Each currency has predefined allowed decimal points that should be taken into consideration when sending the amount check the note after this table.<br>Example: 10000</p> |
| <p><strong>digital_wallet</strong><br>Alpha<br>Mandatory<br>Max: 20</p>             | <p>Digital wallet used for transaction.<br>Possible/ expected values: STCPAY</p>                                                                                                                                                                                                       |
| <p><strong>signature</strong><br>Alphanumeric<br>Mandatory<br>Max: 200</p>          | <p>A string hashed using the Secure Hash Algorithm. Please refer to section <a href="broken-reference">Signature</a><br>Example: 7cad05f0212ed933c9a5d5dffa31661acf2c827a</p>                                                                                                          |
| <p><strong>merchant_identifier</strong><br>Alphanumeric<br>Mandatory<br>Max: 20</p> | <p>The ID of the Merchant.<br>Example: CycHZxVj</p>                                                                                                                                                                                                                                    |
| <p><strong>merchant_reference</strong><br>Alphanumeric<br>Mandatory<br>Max: 40</p>  | <p>The Merchant’s unique order number.<br>Example: XYZ9239-yu898<br>Special characters: - _ .</p>                                                                                                                                                                                      |
| <p><strong>currency</strong><br>Alpha<br>Mandatory<br>Max: 3</p>                    | <p>The currency of the transaction’s amount in ISO code 3.<br>Possible/ expected values: SAR</p>                                                                                                                                                                                       |
| <p><strong>language</strong><br>Alpha<br>Mandatory<br>Max: 2</p>                    | <p>The checkout page and messages language.<br>Possible/ expected values: en/ ar</p>                                                                                                                                                                                                   |
| <p><strong>phone_number</strong><br>Alphanumeric<br>Mandatory<br>max: 19</p>        | <p>The customer's phone number.<br>Example: 0548220713<br>Special characters: + - ( ) <strong>Space</strong></p>                                                                                                                                                                       |

### Generate OTP - Response

**The following parameters will be returned in PayFort's Response:**

| ATTRIBUTES                                                             | Description                                                                                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>service_command</strong><br>Alpha<br>Max: 20</p>            | <p>A command.<br>Possible/ expected values: GENERATE_OTP</p>                                                                                                                                                                                                                                 |
| <p><strong>response_code</strong><br>Numeric<br>Max: 5</p>             | <p>Response Code carries the value of our system's response. *The code consists of five digits, the first 2 digits represent the response <a href="broken-reference">status</a>, and the last 3 digits represent the response <a href="broken-reference">messages</a>.<br>Example: 20064</p> |
| <p><strong>response_message</strong><br>Alphanumeric<br>Max: 150</p>   | <p>The message description of the response code; it returns according to the request language.<br>Possible/ expected values: Please refer to section <a href="broken-reference">messages</a></p>                                                                                             |
| <p><strong>access_code</strong><br>Alphanumeric<br>Max: 20</p>         | <p>Access code.<br>Example: zx0IPmPy5jp1vAz8Kpg7</p>                                                                                                                                                                                                                                         |
| <p><strong>amount</strong><br>Numeric<br>Max: 10</p>                   | <p>The transaction's amount.<br>Example: 10000</p>                                                                                                                                                                                                                                           |
| <p><strong>signature</strong><br>Alphanumeric<br>Max: 200</p>          | <p>A string hashed using the Secure Hash Algorithm. Please refer to section <a href="broken-reference">Signature</a><br>Example: 7cad05f0212ed933c9a5d5dffa31661acf2c827a</p>                                                                                                                |
| <p><strong>merchant_identifier</strong><br>Alphanumeric<br>Max: 20</p> | <p>The ID of the Merchant.<br>Example: CycHZxVj</p>                                                                                                                                                                                                                                          |
| <p><strong>digital_wallet</strong><br>Alpha<br>Max: 20</p>             | <p>Digital wallet used for transaction.<br>Possible/ expected values: STCPAY</p>                                                                                                                                                                                                             |
| <p><strong>merchant_reference</strong><br>Alphanumeric<br>Max: 40</p>  | <p>The Merchant’s unique order number.<br>Example: XYZ9239-yu898</p>                                                                                                                                                                                                                         |
| <p><strong>currency</strong><br>Alpha<br>Max: 3</p>                    | <p>The currency of the transaction’s amount in ISO code 3.<br>Possible/ expected values: SAR</p>                                                                                                                                                                                             |
| <p><strong>language</strong><br>Alpha<br>Max: 2</p>                    | <p>The checkout page and messages language.<br>Possible/ expected values: en/ ar</p>                                                                                                                                                                                                         |
| <p><strong>phone_number</strong><br>Alphanumeric<br>max: 19</p>        | <p>The customer's phone number.<br>Example: 0548220713</p>                                                                                                                                                                                                                                   |

### Purchase URLs

**Test Environment URL:**\
\
Test URL: https://sbpaymentservices.payfort.com/FortAPI/paymentApi\
\
**Production Environment URL:**\
\
Production URL: https://paymentservices.payfort.com/FortAPI/paymentApi\
\


### Parameters Submission Type

REST POST request using JSON.\


### Purchase - Request

**Include the following parameters in the request you will send to Amazon Payment Services:**

```shell
{
    {
    "amount": "68557",
    "digital_wallet": "STCPAY",
    "signature": "{{signature}}",
    "merchant_identifier": "{{merchant_identifier}}",
    "access_code": "FIX7skJDGmjJF0WDh2oB",
    "customer_ip": "127.0.0.1",
    "language": "en",
    "otp": "12345",
    "command": "PURCHASE",
    "merchant_reference": "merchantTest-10117",
    "customer_email": "merchant07@merchantdomain.com",
    "return_url": "http://127.0.0.1/merchantSHEK/payment/stcResponse",
    "currency": "SAR",
    "phone_number": "0551111111",
    "remember_me": "YES"
}
}
```

```php
error_reporting(E_ALL);
ini_set('display_errors', '1');

$url = 'https://sbpaymentservices.payfort.com/FortAPI/paymentApi';

$arrData = array(
    {
        'amount'=> '68557',
    'digital_wallet'=> 'STCPAY',
    'signature'=> '{{signature}}',
    'merchant_identifier'=> '{{merchant_identifier}}',
    'access_code'=> 'FIX7skJDGmjJF0WDh2oB',
    'customer_ip'=> '127.0.0.1',
    'language'=> 'en',
    'otp'=> '12345',
    'command'=> 'PURCHASE',
    'merchant_reference'=> 'merchantTest-10117',
    'customer_email'=> 'merchant07@merchantdomain.com',
    'return_url'=> 'http://127.0.0.1/merchantSHEK/payment/stcResponse',
    'currency'=> 'SAR',
    'phone_number'=> '0551111111',
    'remember_me'=> 'YES'
}

   
);


$ch = curl_init( $url );
# Setup request to send json via POST.
$data = json_encode($arrData);
curl_setopt( $ch, CURLOPT_POSTFIELDS, $data );
curl_setopt( $ch, CURLOPT_HTTPHEADER, array('Content-Type:application/json'));
# Return response instead of printing.
curl_setopt( $ch, CURLOPT_RETURNTRANSFER, true );
# Send request.
$result = curl_exec($ch);
curl_close($ch);
# Print response.
echo "<pre>$result</pre>";
```

```python
import urllib
import urllib2
import json

url = 'https://sbpaymentservices.payfort.com/FortAPI/paymentApi';

arrData = 
    {
        'amount: '68557',
    'digital_wallet: 'STCPAY',
    'signature: '{{signature}}',
    'merchant_identifier: '{{merchant_identifier}}',
    'access_code: 'FIX7skJDGmjJF0WDh2oB',
    'customer_ip: '127.0.0.1',
    'language: 'en',
    'otp: '12345',
    'command: 'PURCHASE',
    'merchant_reference: 'merchantTest-10117',
    'customer_email: 'merchant07@merchantdomain.com',
    'return_url: 'http://127.0.0.1/merchantSHEK/payment/stcResponse',
    'currency: 'SAR',
    'phone_number: '0551111111',
    'remember_me: 'YES'

    
};


values = json.dumps(arrData)
data = urllib.urlencode(values)
req = urllib2.Request(url, data)
response = urllib2.urlopen(req)
page = response.read()
print page + '\n\n'
```

```ruby
require 'json'
require 'net/http'
require 'net/https'
require 'uri'
require 'openssl'
arrData = 

    {
        'amount'=> '68557',
    'digital_wallet'=> 'STCPAY',
    'signature'=> '{{signature}}',
    'merchant_identifier'=> '{{merchant_identifier}}',
    'access_code'=> 'FIX7skJDGmjJF0WDh2oB',
    'customer_ip'=> '127.0.0.1',
    'language'=> 'en',
    'otp'=> '12345',
    'command'=> 'PURCHASE',
    'merchant_reference'=> 'merchantTest-10117',
    'customer_email'=> 'merchant07@merchantdomain.com',
    'return_url'=> 'http://127.0.0.1/merchantSHEK/payment/stcResponse',
    'currency'=> 'SAR',
    'phone_number'=> '0551111111',
    'remember_me'=> 'YES'
}
;
arrData.each {|key, value|
  puts key +value ;
}

arrData = arrData.to_json
uri = URI.parse("https://sbpaymentservices.payfort.com/FortAPI/paymentApi")
http = Net::HTTP.new(uri.host, uri.port)
http.use_ssl = true
http.verify_mode = OpenSSL::SSL::VERIFY_NONE
request = Net::HTTP::Post.new("/v1.1/auth")
request.add_field('Content-Type', 'application/json')
request.body = arrData
response = http.request(request)
```

```java
String jsonRequestString = "{\n    \"amount\": \"68557\",\n    \"digital_wallet\": \"STCPAY\",\n    \"signature\": \"\",\n    \"merchant_identifier\": \"{{merchant_identifier}}\",\n    \"access_code\": \"FIX7skJDGmjJF0WDh2oB\",\n    \"customer_ip\": \"127.0.0.1\",\n    \"language\": \"en\",\n    \"otp\": \"12345\",\n    \"command\": \"PURCHASE\",\n    \"merchant_reference\": \"merchantTest-10117\",\n    \"customer_email\": \"merchant07@merchantdomain.com\",\n    \"return_url\": \"http://127.0.0.1/merchantSHEK/payment/stcResponse\",\n    \"currency\": \"SAR\",\n    \"phone_number\": \"0551111111\",\n    \"remember_me\": \"YES\"\n}";

// Define and Initialize HttpClient
HttpClient httpClient = HttpClientBuilder.create().build();
// Intialize HttpPOST with FORT Payment services URL
HttpPost request = new HttpPost("https://sbpaymentservices.payfort.com/FortAPI/paymentApi");
// Setup Http POST entity with JSON String
StringEntity params = new StringEntity(jsonRequestString);
// Setup request type as JSON
request.addHeader("content-type", "application/json");
request.setEntity(params);
// Post request to FORT
HttpResponse response = httpClient.execute(request);
// Read response using StringBuilder
StringBuilder sb = new StringBuilder();
BufferedReader reader = new BufferedReader(new InputStreamReader(
  response.getEntity().getContent()), 65728);
String line = null;
while ((line = reader.readLine()) != null) {
sb.append(line);
}
// Print response
System.out.println(sb.toString());
```

| ATTRIBUTES                                                                          | Description                                                                                                                                                                                                                                                                        |
| ----------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>command</strong><br>Alpha<br>Mandatory<br>Max: 20</p>                    | <p>A command.<br>Possible/ expected values: PURCHASE</p>                                                                                                                                                                                                                           |
| <p><strong>access_code</strong><br>Alphanumeric<br>Mandatory<br>Max: 20</p>         | <p>Access code.<br>Example: zx0IPmPy5jp1vAz8Kpg7</p>                                                                                                                                                                                                                               |
| <p><strong>digital_wallet</strong><br>Alpha<br>Mandatory<br>Max: 20</p>             | <p>Digital wallet used for transaction.<br>Possible/ expected values: STCPAY</p>                                                                                                                                                                                                   |
| <p><strong>merchant_identifier</strong><br>Alphanumeric<br>Mandatory<br>Max: 20</p> | <p>The ID of the Merchant.<br>Example: CycHZxVj</p>                                                                                                                                                                                                                                |
| <p><strong>merchant_reference</strong><br>Alphanumeric<br>Mandatory<br>Max: 40</p>  | <p>The Merchant’s unique order number.<br>Example: XYZ9239-yu898<br>Special characters: - _ .</p>                                                                                                                                                                                  |
| <p><strong>amount</strong><br>Numeric<br>Mandatory<br>Max: 10</p>                   | <p>The transaction's amount. This needs to be the same as the amount supplied when generating the OTP. *Each currency has predefined allowed decimal points that should be taken into consideration when sending the amount check the note after this table.<br>Example: 10000</p> |
| <p><strong>currency</strong><br>Alpha<br>Mandatory<br>Max: 3</p>                    | <p>The currency of the transaction’s amount in ISO code 3.<br>Possible or Expected Values: SAR</p>                                                                                                                                                                                 |
| <p><strong>token_name</strong><br>Alphanumeric<br>Optional<br>Max: 100</p>          | <p>The Token received from the Tokenization process.<br>Example: Op9Vmp<br>Special characters: . @ - _</p>                                                                                                                                                                         |
| <p><strong>otp</strong><br>Numeric<br>Mandatory<br>Max: 10</p>                      | <p>OTP sent to your customer’s phone number. The length of the OTP can be 4, 5 or 6 characters. During integration, update the OTP field to be dynamic, so it can accept any length.<br>Example: 1234</p>                                                                          |
| <p><strong>language</strong><br>Alpha<br>Mandatory<br>Max: 2</p>                    | <p>The checkout page and messages language.<br>Possible/ expected values: en/ ar</p>                                                                                                                                                                                               |
| <p><strong>customer_email</strong><br>Alphanumeric<br>Mandatory<br>Max: 254</p>     | <p>The customer's email.<br>Example: customer1@domain.com<br>Special characters: _ - . @ +</p>                                                                                                                                                                                     |
| <p><strong>customer_ip</strong><br>Alphanumeric<br>Mandatory<br>max: 45</p>         | <p>It holds the customer's IP address. *It's Mandatory, if the fraud service is active. *We support IPv4 and IPv6 as shown in the example below.<br>Example:<br>IPv4 → 192.178.1.10<br>IPv6 → 2001:0db8:3042:0002:5a55:caff:fef6:bdbf<br>Special characters: . :</p>               |
| <p><strong>signature</strong><br>Alphanumeric<br>Mandatory<br>Max: 200</p>          | <p>A string hashed using the Secure Hash Algorithm. Please refer to section <a href="broken-reference">Signature</a><br>Example: 7cad05f0212ed933c9a5d5dffa31661acf2c827a</p>                                                                                                      |
| <p><strong>order_description</strong><br>Alphanumeric<br>Optional<br>Max: 150</p>   | <p>It holds the description of the order.<br>Example: iPhone 6-S<br>Special characters: <code>'</code> / . _ - # : $ <strong>Space</strong></p>                                                                                                                                    |
| <p><strong>customer_name</strong><br>Alpha<br>Optional<br>Max: 40</p>               | <p>The customer's name.<br>Example: John Smith<br>Special characters: _ \ / - . <code>'</code> <strong>Space</strong></p>                                                                                                                                                          |
| <p><strong>merchant_extra</strong><br>Alphanumeric<br>Optional<br>Max: 999</p>      | <p>Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.<br>Example: JohnSmith<br>Special characters: . ; / _ - , <code>'</code> @</p>                                                                                     |
| <p><strong>merchant_extra1</strong><br>Alphanumeric<br>Optional<br>Max: 250</p>     | <p>Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.<br>Example: JohnSmith<br>Special characters: . ; / _ - , <code>'</code> @</p>                                                                                     |
| <p><strong>merchant_extra2</strong><br>Alphanumeric<br>Optional<br>Max: 250</p>     | <p>Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.<br>Example: JohnSmith<br>Special characters: . ; / _ - , <code>'</code> @</p>                                                                                     |
| <p><strong>merchant_extra3</strong><br>Alphanumeric<br>Optional<br>Max: 250</p>     | <p>Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.<br>Example: JohnSmith<br>Special characters: . ; / _ - , <code>'</code> @</p>                                                                                     |
| <p><strong>merchant_extra4</strong><br>Alphanumeric<br>Optional<br>Max: 250</p>     | <p>Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.<br>Example: JohnSmith<br>Special characters: . ; / _ - , <code>'</code> @</p>                                                                                     |

### Purchase - Response

**The following parameters will be returned in PayFort's Response:**

| ATTRIBUTES                                                                 | Description                                                                                                                                                                                                                                                                                  |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>response_code</strong><br>Numeric<br>Max: 5</p>                 | <p>Response Code carries the value of our system's response. *The code consists of five digits, the first 2 digits represent the response <a href="broken-reference">status</a>, and the last 3 digits represent the response <a href="broken-reference">messages</a>.<br>Example: 20064</p> |
| <p><strong>response_message</strong><br>Alphanumeric<br>Max: 150</p>       | <p>The message description of the response code; it returns according to the request language.<br>Possible/ expected values: Please refer to section <a href="broken-reference">messages</a></p>                                                                                             |
| <p><strong>access_code</strong><br>Alphanumeric<br>Max: 20</p>             | <p>Access code.<br>Example: zx0IPmPy5jp1vAz8Kpg7</p>                                                                                                                                                                                                                                         |
| <p><strong>command</strong><br>Alpha<br>Max: 20</p>                        | <p>A command.<br>Possible/ expected values: PURCHASE</p>                                                                                                                                                                                                                                     |
| <p><strong>digital_wallet</strong><br>Alpha<br>Max: 20</p>                 | <p>Digital wallet used for transaction.<br>Possible/ expected values: STCPAY</p>                                                                                                                                                                                                             |
| <p><strong>merchant_identifier</strong><br>Alphanumeric<br>Max: 20</p>     | <p>The ID of the Merchant.<br>Example: CycHZxVj</p>                                                                                                                                                                                                                                          |
| <p><strong>merchant_reference</strong><br>Alphanumeric<br>Max: 40</p>      | <p>The Merchant’s unique order number.<br>Example: XYZ9239-yu898</p>                                                                                                                                                                                                                         |
| <p><strong>amount</strong><br>Numeric<br>Max: 10</p>                       | <p>The transaction's amount.<br>Example: 10000</p>                                                                                                                                                                                                                                           |
| <p><strong>currency</strong><br>Alpha<br>Max: 3</p>                        | <p>The currency of the transaction’s amount in ISO code 3.<br>Possible or Expected Values: SAR</p>                                                                                                                                                                                           |
| <p><strong>language</strong><br>Alpha<br>Max: 2</p>                        | <p>The checkout page and messages language.<br>Possible/ expected values: en/ ar</p>                                                                                                                                                                                                         |
| <p><strong>customer_email</strong><br>Alphanumeric<br>Max: 254</p>         | <p>The customer's email.<br>Example: customer1@domain.com</p>                                                                                                                                                                                                                                |
| <p><strong>customer_ip</strong><br>Alphanumeric<br>max: 45</p>             | <p>It holds the customer's IP address. *We support IPv4 and IPv6 as shown in the example below.<br>Example:<br>IPv4 → 192.178.1.10<br>IPv6 → 2001:0db8:3042:0002:5a55:caff:fef6:bdbf</p>                                                                                                     |
| <p><strong>signature</strong><br>Alphanumeric<br>Mandatory<br>Max: 200</p> | <p>A string hashed using the Secure Hash Algorithm. Please refer to section <a href="broken-reference">Signature</a><br>Example: 7cad05f0212ed933c9a5d5dffa31661acf2c827a</p>                                                                                                                |
| <p><strong>eci</strong><br>Alpha<br>Max: 16</p>                            | <p>Ecommerce indicator.<br>Possible/ expected values: ECOMMERCE</p>                                                                                                                                                                                                                          |
| <p><strong>payment_option</strong><br>Alpha<br>Max: 10</p>                 | <p>Payment option.<br>Possible/ expected values: STCPAY<br></p>                                                                                                                                                                                                                              |
| <p><strong>fort_id</strong><br>Numeric<br>Max: 20</p>                      | <p>The order's unique reference returned by our system.<br>Example: 149295435400084008</p>                                                                                                                                                                                                   |
| <p><strong>status</strong><br>Numeric<br>Max: 2</p>                        | <p>A two-digit numeric value that indicates the status of the transaction.<br>Possible/ expected values: Please refer to section <a href="broken-reference">statuses</a></p>                                                                                                                 |
| <p><strong>token_name</strong><br>Alphanumeric<br>max: 100</p>             | <p>The Token received from the Tokenization process.<br>Example: COp9Vmp</p>                                                                                                                                                                                                                 |
| <p><strong>order_description</strong><br>Alphanumeric<br>Max: 150</p>      | <p>A description of the order.<br>Example: iPhone 6-S</p>                                                                                                                                                                                                                                    |
| <p><strong>customer_name</strong><br>Alpha<br>Max: 40</p>                  | <p>The customer's name.<br>Example: John Smith</p>                                                                                                                                                                                                                                           |
| <p><strong>merchant_extra</strong><br>Alphanumeric<br>Max: 999</p>         | <p>Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.<br>Example: JohnSmith</p>                                                                                                                                                   |
| <p><strong>merchant_extra1</strong><br>Alphanumeric<br>Max: 250</p>        | <p>Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.<br>Example: JohnSmith</p>                                                                                                                                                   |
| <p><strong>merchant_extra2</strong><br>Alphanumeric<br>Max: 250</p>        | <p>Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.<br>Example: JohnSmith</p>                                                                                                                                                   |
| <p><strong>merchant_extra3</strong><br>Alphanumeric<br>Max: 250</p>        | <p>Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.<br>Example: JohnSmith</p>                                                                                                                                                   |
| <p><strong>merchant_extra4</strong><br>Alphanumeric<br>Max: 250</p>        | <p>Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.<br>Example: JohnSmith</p>                                                                                                                                                   |

Was this helpful? Yes NoThank you for helping improve Amazon Payment Services' documentation. If you need help or have any questions,Get In Touchor contact us on integration-ps@amazon.com.
