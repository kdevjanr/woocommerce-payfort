# ValU Consumer Finance

ValU consumer finance is a simple and secure financing platform where your customers can do online purchases on short-term financing and repay the amount based on specific installment plans at an interest rate offered by the financing company. For now, we have partnered with **ValU** in Egypt to offer consumer financing services.

## Before Starting

Before you start, remember:

1. Your customer should be registered with **ValU** in order to have this benefit of installments.
2. You should have a valid SHA signature, to configure signatures, refer [Signature](https://paymentservices-reference.payfort.com/docs/api/build/index.html#signature) and [Signature Calculation Tool](https://paymentservices-reference.payfort.com/docs/api/build/index.html#try-it-yourself).
3. To fetch your merchant reference and merchant access code, go to Merchant Management, search and select the test merchant account and click Security Settings.

## OTP Generate

This request to generate an OTP for the customer, where the customer should fill down his phone number in the merchant’s check-out page. ValU will generate the OTP code and send it to customer as SMS.

## Purchase

This request allows the customer to purchase his selected items. [https://paymentservices.payfort.com/FortAPI/paymentApi](https://paymentservices.payfort.com/FortAPI/paymentApi)

## URLs

**Test Environment URL:** https://sbpaymentservices.payfort.com/FortAPI/paymentApi

**Production Environment URL:** https://paymentservices.payfort.com/FortAPI/paymentApi

## OTP Generate

You can now generate an OTP for the customer, where the customer should fill in their phone number in the merchant’s check-out page. ValU will generate the OTP code and send it to customer as SMS.

### OTP Generate – Request

```php
error_reporting(E_ALL);
ini_set('display_errors', '1');

$url = 'https://sbpaymentservices.payfort.com/FortAPI/paymentApi';

$arrData = array(
   'merchant_reference'=>'TEST-009967',
    'merchant_identifier'=>'CycHZxVj', 
    'access_code'=>'zx0IPmPy5jp1vAz8Kpg7',
    'signature'=>'27c1303138f8718e56f311d1b3d823b5a644e6bcd4fac43d5454955b13b5b337',
    'service_command'=>'OTP_GENERATE',
    'language'=>'en',
    'payment_option'=>'VALU',
    'phone_number'=>'01220422223',
    'amount'=>'100000',
    'currency'=>'EGP',
    'include_installments'=>'YES',
    'wallet_amount'=>'500000',
    'cashback_wallet_amount'=>'300000'
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
   'merchant_reference':'TEST-009967',
    'merchant_identifier':'CycHZxVj', 
    'access_code':'zx0IPmPy5jp1vAz8Kpg7',
    'signature':'27c1303138f8718e56f311d1b3d823b5a644e6bcd4fac43d5454955b13b5b337',
    'service_command':'OTP_GENERATE',
    'language':'en',
    'payment_option':'VALU',
    'phone_number':'01220422223',
    'amount':'100000',
    'currency':'EGP',
    'include_installments':'YES',
    'wallet_amount':'500000',
    'cashback_wallet_amount':'300000'
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
arrData = {
   'merchant_reference'=>'TEST-009967',
    'merchant_identifier'=>'CycHZxVj', 
    'access_code'=>'zx0IPmPy5jp1vAz8Kpg7',
    'signature'=>'27c1303138f8718e56f311d1b3d823b5a644e6bcd4fac43d5454955b13b5b337',
    'service_command'=>'OTP_GENERATE',
    'language'=>'en',
    'payment_option'=>'VALU',
    'phone_number'=>'01220422223',
    'amount'=>'100000',
    'currency'=>'EGP',
    'include_installments'=>'YES',
    'wallet_amount'=>'500000',
    'cashback_wallet_amount'=>'300000'
};
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
String jsonRequestString = "{\n    \"merchant_reference\":\"TEST-009967\",\n    \"merchant_identifier\":\"CycHZxVj\", \n    \"access_code\":\"zx0IPmPy5jp1vAz8Kpg7\",\n    \"signature\":\"27c1303138f8718e56f311d1b3d823b5a644e6bcd4fac43d5454955b13b5b337\",\n    \"service_command\":\"OTP_GENERATE\",\n    \"language\":\"en\",\n    \"payment_option\":\"VALU\",\n    \"phone_number\":\"01220422223\",\n    \"amount\":\"100000\",\n    \"currency\":\"EGP\",\n    \"include_installments\":\"YES\",\n    \"wallet_amount\":\"500000\",\n    \"cashback_wallet_amount\":\"300000\"\n}";

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

```shell
 {
 "merchant_reference":"TEST-009967",
    "merchant_identifier":"CycHZxVj", 
    "access_code":"zx0IPmPy5jp1vAz8Kpg7",
    "signature":"27c1303138f8718e56f311d1b3d823b5a644e6bcd4fac43d5454955b13b5b337",
    "service_command":"OTP_GENERATE",
    "language":"en",
    "payment_option":"VALU",
    "phone_number":"01220422223",
    "amount":"100000",
    "currency":"EGP",
    "include_installments":"YES",
    "wallet_amount":"500000",
    "cashback_wallet_amount":"300000"
}
```

**OTP Generate Request Parameters**

| Parameter Name                                                                      | Description                                                                                                                                                                                                                                                                                                                                                                                    |
| ----------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>service_command</strong><br>Alpha<br>Mandatory<br>Max: 20</p>            | <p>Command.<br>Posssible values: OTP_GENERATE</p>                                                                                                                                                                                                                                                                                                                                              |
| <p><strong>access_code</strong><br>Alphanumeric<br>Mandatory<br>Max: 20</p>         | Access code. Example: zx0IPmPy5jp1vAz8Kp g7                                                                                                                                                                                                                                                                                                                                                    |
| <p><strong>merchant_identifier</strong><br>Alphanumeric<br>Mandatory<br>Max: 20</p> | <p>The ID of the Merchant.<br>Example: CycHZxVj</p>                                                                                                                                                                                                                                                                                                                                            |
| <p><strong>merchant_reference</strong><br>Alphanumeric<br>Mandatory<br>Max: 40</p>  | <p>The Merchant’s unique order number. The merchant reference should be the same for all APIs.<br>For example: XYZ9239yu898</p>                                                                                                                                                                                                                                                                |
| <p><strong>language</strong><br>Alpha<br>Mandatory<br>Max: 2</p>                    | <p>The checkout page and messages language. Possible values:<br>- en<br>- ar</p>                                                                                                                                                                                                                                                                                                               |
| <p><strong>payment_option</strong><br>Alpha<br>Mandatory<br>Max: 10</p>             | <p>Payment option.<br>Possible values: VALU</p>                                                                                                                                                                                                                                                                                                                                                |
| <p><strong>include_installments</strong><br>Alpha<br>Optional<br>Max: 3</p>         | <p>Defines whether the customer can pay in installments.<br>Possible Values YES/NO. Default Value is YES.</p>                                                                                                                                                                                                                                                                                  |
| <p><strong>total_downpayment</strong><br>Numeric<br>Optional<br>Max: 100</p>        | <p>Defines the total down-payment amount payable by the customer. *Decimal values are not accepted.<br>For example:1200</p>                                                                                                                                                                                                                                                                    |
| <p><strong>phone_number</strong><br>Alphanumeric<br>Mandatory<br>Max: 19</p>        | <p>The customer’s phone number registered for ValU.<br>For example:</p><p>00008557694</p>                                                                                                                                                                                                                                                                                                      |
| <p><strong>amount</strong><br>Numeric<br>Mandatory<br>Max: 10</p>                   | <p>The transaction’s amount. *Each currency has predefined allowed decimal points that should be taken into consideration when sending the amount.<br>For example: 10000</p>                                                                                                                                                                                                                   |
| <p><strong>currency</strong><br>Alpha<br>Mandatory<br>Max: 3</p>                    | <p>The currency of the transaction amount in ISO code 3.<br>For example: EGP</p>                                                                                                                                                                                                                                                                                                               |
| <p><strong>signature</strong><br>Alphanumeric<br>Mandatory<br>Max: 200</p>          | <p>A string hashed using the Secure Hash Algorithm. Please refer to section <a href="broken-reference">Signature</a><br>.<br>For example,7cad05f0212ed933c9a5d5dffa31661acf2c827a</p>                                                                                                                                                                                                          |
| <p><strong>merchant_extra1</strong><br>Alphanumeric<br>Optional<br>Max: 250</p>     | <p>Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.<br>Special characters.;/_-,'@<br>For example: JohnSmith</p>                                                                                                                                                                                                                   |
| <p><strong>merchant_extra2</strong><br>Alphanumeric<br>Optional<br>Max: 250</p>     | <p>Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.<br>Special characters.;/_-,'@<br>JohnSmith</p>                                                                                                                                                                                                                                |
| <p><strong>merchant_extra3</strong><br>Alphanumeric<br>Optional<br>Max: 250</p>     | <p>Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.<br>Special characters.;/_-,'@<br>For example: JohnSmith</p>                                                                                                                                                                                                                   |
| <p><strong>wallet_amount</strong><br>Numeric<br>Mandatory<br>Max:10</p>             | <p>Wallet amount or ToU is a gift balance that you can purchase using your valU limit and can pay in flexible installment plans from 6-60 months. You can transfer ToU balance to all of your loved ones, they don’t need to be valU customers. *Each currency has predefined allowed decimal points that should be taken into consideration when sending the amount.<br>For example:10000</p> |
| <p><strong>cashback_wallet_amount</strong><br>Numeric<br>Mandatory<br>Max:10</p>    | <p>Amount stored in cashback wallet. *Each currency has predefined allowed decimal points that should be taken into consideration when sending the amount.<br>For example:10000</p>                                                                                                                                                                                                            |

### OTP Generate – Response

> Generate Response Example

**OTP Generate Response Parameters**

| Parameter Name                                                                   | Description                                                                                                                                                                                                                                                                                                                                                                                    |
| -------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>service_command</strong><br>Alpha<br>Max: 20</p>                      | <p>Command.<br>For example: OTP_GENERATE</p>                                                                                                                                                                                                                                                                                                                                                   |
| <p><strong>access_code</strong><br>Alphanumeric<br>Max: 20</p>                   | <p>Access code.<br>For example: zx0IPmPy5jp1vAz8Kpg7</p>                                                                                                                                                                                                                                                                                                                                       |
| <p><strong>merchant_identifier</strong><br>Alphanumeric<br>Max: 20</p>           | <p>The ID of the Merchant.<br>For example: CycHZxVj</p>                                                                                                                                                                                                                                                                                                                                        |
| <p><strong>merchant_reference</strong><br>Alphanumeric<br>Max: 40</p>            | <p>The Merchant’s unique order number.<br>For example:XYZ2939-yu898</p>                                                                                                                                                                                                                                                                                                                        |
| <p><strong>language</strong><br>Alpha<br>Max: 2</p>                              | <p>The checkout page and messages language.For example:<br>- en<br>- ar</p>                                                                                                                                                                                                                                                                                                                    |
| <p><strong>payment_option</strong><br>Alpha<br>10</p>                            | <p>Payment option.<br>For example:VALU</p>                                                                                                                                                                                                                                                                                                                                                     |
| <p><strong>phone_number</strong><br>Alphanumeric<br>Max: 19<br></p>              | <p>The customer’s phone number registered for ValU.<br>For example: 00008557694</p>                                                                                                                                                                                                                                                                                                            |
| <p><strong>merchant_order_id</strong><br>Alphanumeric<br>100</p>                 | <p>The Merchant’s unique order id. * It should be unique per each transaction and you should use the same merchant_order_id value for all APIs.<br>For example: Valu123</p>                                                                                                                                                                                                                    |
| <p><strong>amount</strong><br>Numeric<br>Max: 10</p>                             | <p>The transaction’s amount. *Each currency has predefined allowed decimal points that should be taken into consideration when sending the amount.<br>For example: 10000</p>                                                                                                                                                                                                                   |
| <p><strong>currency</strong><br>Alpha<br>Max: 3</p>                              | <p>The currency of the transaction amount in ISO code 3.<br>For example:EGP</p>                                                                                                                                                                                                                                                                                                                |
| <p><strong>total_downpayment</strong><br>Numeric<br>Max: 100</p>                 | <p>Defines the total down-payment amount payable by the customer.<br>For example: 10000</p>                                                                                                                                                                                                                                                                                                    |
| <p><strong>installment_detail</strong><br>List</p>                               | Defines installment plan details as selected by the customer. This is displayed if include\_installments is set to YES. Lists the fee amount, installment amount, installment per month and total installment.                                                                                                                                                                                 |
| <p><strong>signature</strong><br>Alphanumeric<br>Max: 200</p>                    | <p>A string hashed using the Secure Hash Algorithm. Please refer to section <a href="broken-reference">Signature</a><br>For example: 7cad05f0212ed933c9a5d5dffa31661acf2c827a</p>                                                                                                                                                                                                              |
| <p><strong>merchant_extra1</strong><br>Alphanumeric<br>Max: 250</p>              | <p>Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.<br>For example: JohnSmith</p>                                                                                                                                                                                                                                                 |
| <p><strong>merchant_extra2</strong><br>Alphanumeric<br>Max: 250</p>              | Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.                                                                                                                                                                                                                                                                                  |
| <p><strong>merchant_extra3</strong><br>Alphanumeric<br>Max: 250</p>              | Extra data sent by merchant. Will be received and sent back as received. Will not be displayed in any report.                                                                                                                                                                                                                                                                                  |
| <p><strong>response_message</strong><br>Alphanumeric<br>Max: 150</p>             | Message description of the response code. It returns according to the request language. Please refer to section [messages](broken-reference)                                                                                                                                                                                                                                                   |
| <p><strong>response_code</strong><br>Numeric<br>Max: 5</p>                       | <p>Response code carries the value of our system's response.</p><p>*The code consists of five digits, the first 2 digits represent the response status, and the last 3 digits represent the response message.<br>For example: 88000<br></p>                                                                                                                                                    |
| <p><strong>status</strong><br>Numeric<br>Max: 2</p>                              | A two-digit numeric value that indicates the status of the transaction.Please refer to section [statuses](broken-reference).                                                                                                                                                                                                                                                                   |
| <p><strong>wallet_amount</strong><br>Numeric<br>Mandatory<br>Max:10</p>          | <p>Wallet amount or ToU is a gift balance that you can purchase using your valU limit and can pay in flexible installment plans from 6-60 months. You can transfer ToU balance to all of your loved ones, they don’t need to be valU customers. *Each currency has predefined allowed decimal points that should be taken into consideration when sending the amount.<br>For example:10000</p> |
| <p><strong>cashback_wallet_amount</strong><br>Numeric<br>Mandatory<br>Max:10</p> | <p>Amount stored in cashback wallet. *Each currency has predefined allowed decimal points that should be taken into consideration when sending the amount.<br>For example:10000</p>                                                                                                                                                                                                            |

## Purchase

This request allows the Customer to Purchase his selected items through the selected consumer finance.

\###Purchase – Request

> Purchase Request Example

```php
error_reporting(E_ALL);
ini_set('display_errors', '1');

$url = 'https://sbpaymentservices.payfort.com/FortAPI/paymentApi';
$arrData = array(
'merchant_reference'=>'XYZ9239-yu898', 
'merchant_identifier'=>'CycHZxVj', 
'access_code'=>'zx0IPmPy5jp1vAz8Kpg7',
'signature'=>'b574e362cc08d7504d8277e71400132f06064ee1537cd570717569b583dec0b5', 
'command'=>'PURCHASE',
'language'=>'en',
'payment_option'=>'VALU', 
'phone_number'=>'00008557694', 
'amount'=>'10000',
'currency'=>'EGP', 
'customer_email'=>'customer@domain.com', 
'otp'=>'123456',
'tenure'=>'6', 
'total_down_payment'=>'1200',
'purchase_description'=>'Test',
'wallet_amount'=>'500000',
'cashback_wallet_amount'=>'300000'
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
'merchant_reference':'XYZ9239-yu898', 
'merchant_identifier':'CycHZxVj', 
'access_code':'zx0IPmPy5jp1vAz8Kpg7',
'signature':'b574e362cc08d7504d8277e71400132f06064ee1537cd570717569b583dec0b5', 
'command':'PURCHASE',
'language':'en',
'payment_option':'VALU', 
'phone_number':'00008557694', 
'amount':'10000',
'currency':'EGP', 
'customer_email':'customer@domain.com', 
'otp':'123456',
'tenure':'6', 
'total_down_payment':'1200',
'purchase_description':'Test',
'wallet_amount':'500000',
'cashback_wallet_amount':'300000'
    
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

arrData = {
    'merchant_reference'=>'XYZ9239-yu898', 
'merchant_identifier'=>'CycHZxVj', 
'access_code'=>'zx0IPmPy5jp1vAz8Kpg7',
'signature'=>'b574e362cc08d7504d8277e71400132f06064ee1537cd570717569b583dec0b5', 
'command'=>'PURCHASE',
'language'=>'en',
'payment_option'=>'VALU', 
'phone_number'=>'00008557694', 
'amount'=>'10000',
'currency'=>'EGP', 
'customer_email'=>'customer@domain.com', 
'otp'=>'123456',
'tenure'=>'6', 
'total_down_payment'=>'1200',
'purchase_description'=>'Test',
'wallet_amount'=>'500000',
'cashback_wallet_amount'=>'300000'
};
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
String jsonRequestString = "{\n    \"merchant_reference\":\"TEST-009967\",\n    \"merchant_identifier\":\"CycHZxVj\", \n    \"access_code\":\"zx0IPmPy5jp1vAz8Kpg7\",\n    \"signature\":\"27c1303138f8718e56f311d1b3d823b5a644e6bcd4fac43d5454955b13b5b337\",\n    \"service_command\":\"OTP_GENERATE\",\n    \"language\":\"en\",\n    \"payment_option\":\"VALU\",\n    \"phone_number\":\"01220422223\",\n    \"amount\":\"100000\",\n    \"currency\":\"EGP\",\n    \"include_installments\":\"YES\",\n    \"wallet_amount\":\"500000\",\n    \"cashback_wallet_amount\":\"300000\"\n}";

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

```shell
 {
    
"merchant_reference":"XYZ9239-yu898", 
"merchant_identifier":"CycHZxVj", 
"access_code":"zx0IPmPy5jp1vAz8Kpg7",
"signature":"b574e362cc08d7504d8277e71400132f06064ee1537cd570717569b583dec0b5", 
"command":"PURCHASE",
"language":"en",
"payment_option":"VALU", 
"phone_number":"00008557694", 
"amount":"10000",
"currency":"EGP", 
"customer_email":"customer@domain.com", 
"otp":"123456",
"tenure":"6", 
"total_down_payment":"1200",
"purchase_description":"Test",
"wallet_amount":"500000",
"cashback_wallet_amount":"300000"

}
```

**Purchase Request Parameters**

| Parameter Name                                                                        | Description                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>command</strong><br>Alpha<br>Mandatory<br>Max: 20</p>                      | <p>Command.<br>Possible values: PURCHASE</p>                                                                                                                                                                                                                                                                                                                                                   |
| <p><strong>access_code</strong><br>Alphanumeric<br>Mandatory<br>Max: 20</p>           | Access code.                                                                                                                                                                                                                                                                                                                                                                                   |
| <p><strong>merchant_identifier</strong><br>Alphanumeric<br>Mandatory<br>Max: 20</p>   | <p>The ID of the Merchant.<br>For example: CycHZxVj</p>                                                                                                                                                                                                                                                                                                                                        |
| <p><strong>merchant_reference</strong><br>Alphanumeric<br>Mandatory<br>Max:40</p>     | <p>The Merchant’s unique order number. The merchant reference should be the same for all APIs.<br>-_.<br>For example: XYZ9239-yu898</p>                                                                                                                                                                                                                                                        |
| <p><strong>payment_option</strong><br>Alpha<br>Mandatory<br>Max: 10</p>               | <p>Payment option.<br>Possible Values: VALU</p>                                                                                                                                                                                                                                                                                                                                                |
| <p><strong>phone_number</strong><br>Alphanumeric<br>Mandatory<br>19</p>               | <p>The customer’s phone number registered for ValU.<br>For example: 00008557694</p>                                                                                                                                                                                                                                                                                                            |
| <p><strong>amount</strong><br>Numeric<br>Mandatory<br>Max: 10</p>                     | <p>The transaction's amount.Each currency has predefined allowed decimal points that should be taken into consideration when sending the amount.<br>For example: 10000</p>                                                                                                                                                                                                                     |
| <p><strong>currency</strong><br>Alpha<br>Mandatory<br>Max: 3</p>                      | <p>The currency of the transaction’s amount in ISO code 3.<br>For example: EGP</p>                                                                                                                                                                                                                                                                                                             |
| <p><strong>language</strong><br>Alpha<br>Mandatory<br>Max: 2</p>                      | <p>The checkout page and messages language.For example<br>- en<br>- ar</p>                                                                                                                                                                                                                                                                                                                     |
| <p><strong>customer_email</strong><br>Alphanumeric<br>Mandatory<br>Max:254</p>        | <p>The customer's email.<br>Special Characters: _-.@+<br>For example:</p><p>customer@domain.com</p>                                                                                                                                                                                                                                                                                            |
| <p><strong>otp</strong><br>Alphanumeric<br>Mandatory<br>Max: 10</p>                   | <p>OTP sent by mobile.<br>For example, 123456</p>                                                                                                                                                                                                                                                                                                                                              |
| <p><strong>tenure</strong><br>Alphanumeric<br>Mandatory<br>Max: 100</p>               | <p>The tenure for the installment payments.<br>For example: 6</p>                                                                                                                                                                                                                                                                                                                              |
| <p><strong>signature</strong><br>Alphanumeric<br>Mandatory<br>Max: 200</p>            | <p>A string hashed using the Secure Hash Algorithm. Please refer to section <a href="broken-reference">Signature</a><br><br>For example: 7cad05f0212ed933c9a5d5dffa31661acf2c827a</p>                                                                                                                                                                                                          |
| <p><strong>purchase_ description</strong><br>Alphanumeric<br>Mandatory<br>Max:100</p> | <p>The purchase description.<br>For example: Test</p>                                                                                                                                                                                                                                                                                                                                          |
| <p><strong>total_down_payment</strong><br>Alphanumeric<br>Mandatory<br>Max:100</p>    | The total transaction’s down payment.Decimal values are not accepted.For example:0                                                                                                                                                                                                                                                                                                             |
| <p><strong>wallet_amount</strong><br>Numeric<br>Mandatory<br>Max:10</p>               | <p>Wallet amount or ToU is a gift balance that you can purchase using your valU limit and can pay in flexible installment plans from 6-60 months. You can transfer ToU balance to all of your loved ones, they don’t need to be valU customers. *Each currency has predefined allowed decimal points that should be taken into consideration when sending the amount.<br>For example:10000</p> |
| <p><strong>cashback_wallet_amount</strong><br>Numeric<br>Mandatory<br>Max:10</p>      | <p>Amount stored in cashback wallet. *Each currency has predefined allowed decimal points that should be taken into consideration when sending the amount.<br>For example:10000</p>                                                                                                                                                                                                            |

### Purchase – Response

> Purchase Response Example

**Purchase Response Parameters**

| Parameter Name                                                                   | Description                                                                                                                                                                                                                                                                                                                                                                                    |
| -------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>command</strong><br>Alpha<br>Max:20</p>                               | <p>Command.<br>Possible Values: PURCHASE</p>                                                                                                                                                                                                                                                                                                                                                   |
| <p><strong>access_code</strong><br>Alphanumeric<br>Max: 20</p>                   | <p>Access code.<br>For example: zx0IPmPy5jp1vAz8Kpg7</p>                                                                                                                                                                                                                                                                                                                                       |
| <p><strong>merchant_identifier</strong><br>Alphanumeric<br>Max: 20</p>           | <p>The ID of the Merchant.<br>For example: CycHZxVj</p>                                                                                                                                                                                                                                                                                                                                        |
| <p><strong>merchant_reference</strong><br>Alphanumeric<br>Max: 40</p>            | <p>The Merchant’s unique order number.<br>For example: XYZ2939-yu898</p>                                                                                                                                                                                                                                                                                                                       |
| <p><strong>payment_option</strong><br>Alpha<br>Max:10</p>                        | <p>Payment option.<br>Possible values: VALU</p>                                                                                                                                                                                                                                                                                                                                                |
| <p><strong>phone_number</strong><br>Alphanumeric<br>Max: 19</p>                  | <p>The customer’s phone number registered for ValU.<br>For example: 00008557694</p>                                                                                                                                                                                                                                                                                                            |
| <p><strong>amount</strong><br>Numeric<br>Max:10</p>                              | <p>The transaction’s amount. *Each currency has predefined allowed decimal points that should be taken into consideration when sending the amount.<br>For example: 10000</p>                                                                                                                                                                                                                   |
| <p><strong>currency</strong><br>Alpha<br>Max: 3</p>                              | <p>The currency of the transaction’s amount in ISO code 3.<br>For example: EGP</p>                                                                                                                                                                                                                                                                                                             |
| <p><strong>language</strong><br>Alpha<br>Max:2</p>                               | <p>The checkout page and messages language.For example<br>- en<br>- ar</p>                                                                                                                                                                                                                                                                                                                     |
| <p><strong>customer_email</strong><br>Alphanumeric<br>Max: 254</p>               | <p>The customer's email.<br>For example: <a href="mailto:customer@domain.com">customer@domain.com</a></p>                                                                                                                                                                                                                                                                                      |
| <p><strong>signature</strong><br>Alphanumeric<br>Max:200</p>                     | <p>A string hashed using the Secure Hash Algorithm. Please refer to section <a href="broken-reference">Signature</a><br><br>For example: 7cad05f0212ed933c9a5d5dffa31661acf2c827a</p>                                                                                                                                                                                                          |
| <p><strong>purchase_description</strong><br>Alphanumeric<br>Max:100</p>          | <p>The purchase description.<br>For example: Test</p>                                                                                                                                                                                                                                                                                                                                          |
| <p><strong>customer_ip</strong><br>Alphanumeric<br>Max:45</p>                    | <p>It holds the customer's IP address.</p><p>*We support IPv4 and IPv6 as shown in the example on the right hand side.</p><p><strong>IPv4</strong>è192.17 8.1.10</p><p><strong>IPv6</strong>è2001:0db8:3042:0002:5a55:caff:fef6:bdbf</p>                                                                                                                                                       |
| <p><strong>eci</strong><br>Alpha<br>Max:16</p>                                   | <p>E-commerce indicator.<br>Possible values: ECOMMERCE</p>                                                                                                                                                                                                                                                                                                                                     |
| <p><strong>fort_id</strong><br>Numeric<br>Max: 20</p>                            | The order's unique reference returned by our system.For example: 149295435400084008                                                                                                                                                                                                                                                                                                            |
| <p><strong>response_message</strong><br>Alphanumeric<br>Max:150</p>              | Message description of the response code. It returns according to the request language. Please refer to section [messages](broken-reference)                                                                                                                                                                                                                                                   |
| <p><strong>response_code</strong><br>Numeric<br>Max:5</p>                        | <p>Response code carries the value of our system's response.</p><p>*The code consists of five digits, the first 2 digits represent the response status, and the last 3 digits represent the response message.</p><p><br>For example: 14000</p>                                                                                                                                                 |
| <p><strong>status</strong><br>Numeric<br>Max: 2<br></p>                          | A two-digit numeric value that indicates the status of the transaction. Please refer to section [statuses](broken-reference).                                                                                                                                                                                                                                                                  |
| <p><strong>wallet_amount</strong><br>Numeric<br>Mandatory<br>Max:10</p>          | <p>Wallet amount or ToU is a gift balance that you can purchase using your valU limit and can pay in flexible installment plans from 6-60 months. You can transfer ToU balance to all of your loved ones, they don’t need to be valU customers. *Each currency has predefined allowed decimal points that should be taken into consideration when sending the amount.<br>For example:10000</p> |
| <p><strong>cashback_wallet_amount</strong><br>Numeric<br>Mandatory<br>Max:10</p> | <p>Amount stored in cashback wallet. *Each currency has predefined allowed decimal points that should be taken into consideration when sending the amount.<br>For example:10000</p>                                                                                                                                                                                                            |
| <p><strong>loan_number</strong><br>Alphanumeric<br>Max:100</p>                   | Number generated by Valu for each successful purchase transaction.                                                                                                                                                                                                                                                                                                                             |
| <p><strong>valu_transaction_id</strong><br>Alphanumeric<br>Max:100</p>           | Unique identifier for the transaction.                                                                                                                                                                                                                                                                                                                                                         |

## Refund API

The refund API has been implemented to follow the same standards for all the other payment option refund flow. Please use the following document to understand the flow: [https://docs.payfort.com/docs/api/build/index.html#refund-operation](https://docs.payfort.com/docs/api/build/index.html#refund-operation)

Note; The refund API of ValU supports the full refund and partial.

## Get Installment Plans Request

Using this API, you can fetch the installment plans the customer has selected.

> Request Example

```php
error_reporting(E_ALL);
ini_set('display_errors', '1');

$url = 'https://sbpaymentservices.payfort.com/FortAPI/paymentApi';
$arrData = array(
'service_command'=> 'GET_INSTALLMENTS_PLANS',
'merchant_reference'=>'XYZ9239-yu898',
'merchant_identifier'=>'CycHZxVj', 
'access_code'=>'zx0IPmPy5jp1vAz8Kpg7',
'signature'=>'b574e362cc08d7504d8277e71400132f06064ee1537cd570717569b583dec0b5',
'phone_number'=> '01220422223',
'payment_option'=>'VALU',
'language'=> 'en',
'amount'=>'100000',
'total_downpayment'=>'1200',
'wallet_amount'=>'500000',
'cashback_wallet_amount'=>'300000'
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
    'service_command': 'GET_INSTALLMENTS_PLANS',
'merchant_reference':'XYZ9239-yu898',
'merchant_identifier':'CycHZxVj', 
'access_code':'zx0IPmPy5jp1vAz8Kpg7',
'signature':'b574e362cc08d7504d8277e71400132f06064ee1537cd570717569b583dec0b5',
'phone_number': '01220422223',
'payment_option':'VALU',
'language': 'en',
'amount':'100000',
'total_downpayment':'1200',
'wallet_amount':'500000',
'cashback_wallet_amount':'300000'
    
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

arrData = {
    'service_command'=> 'GET_INSTALLMENTS_PLANS',
'merchant_reference'=>'XYZ9239-yu898',
'merchant_identifier'=>'CycHZxVj', 
'access_code'=>'zx0IPmPy5jp1vAz8Kpg7',
'signature'=>'b574e362cc08d7504d8277e71400132f06064ee1537cd570717569b583dec0b5',
'phone_number'=> '01220422223',
'payment_option'=>'VALU',
'language'=> 'en',
'amount'=>'100000',
'total_downpayment'=>'1200',
'wallet_amount'=>'500000',
'cashback_wallet_amount'=>'300000'
};
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
String jsonRequestString = "{\n\"service_command\": \"GET_INSTALLMENTS_PLANS\",\n\"merchant_reference\":\"XYZ9239-yu898\",\n\"merchant_identifier\":\"CycHZxVj\", \n\"access_code\":\"zx0IPmPy5jp1vAz8Kpg7\",\n\"signature\":\"b574e362cc08d7504d8277e71400132f06064ee1537cd570717569b583dec0b5\",\n\"phone_number\": \"01220422223\",\n\"payment_option\":\"VALU\",\n\"language\": \"en\",\n\"amount\":\"100000\",\n\"total_downpayment\":\"1200\",\n\"wallet_amount\":\"500000\",\n\"cashback_wallet_amount\":\"300000\"\n\n}";

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

```shell
 {
    
"service_command": "GET_INSTALLMENTS_PLANS",
"merchant_reference":"XYZ9239-yu898",
"merchant_identifier":"CycHZxVj", 
"access_code":"zx0IPmPy5jp1vAz8Kpg7",
"signature":"b574e362cc08d7504d8277e71400132f06064ee1537cd570717569b583dec0b5",
"phone_number": "01220422223",
"payment_option":"VALU",
"language": "en",
"amount":"100000",
"total_downpayment":"1200",
"wallet_amount":"500000",
"cashback_wallet_amount":"300000"
}

```

**Get Installment Plan Parameters**

| Parameter Name                                                                      | Description                                                                                                                                                                                                                                                                                                                                                                                    |
| ----------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>service_command</strong><br>Alpha<br>Mandatory<br>Max:20</p>             | <p>Command.<br>For example:GET_INSTALLMENTS_PLANS</p>                                                                                                                                                                                                                                                                                                                                          |
| <p><strong>access_code</strong><br>Alphanumeric<br>Mandatory<br>Max:20</p>          | <p>Access code.<br>For example:zx0IPmPy5jp1vAz8Kpg7</p>                                                                                                                                                                                                                                                                                                                                        |
| <p><strong>merchant_identifier</strong><br>Alphanumeric<br>Mandatory<br>Max: 20</p> | <p>The ID of the Merchant.<br>For example: CycHZxVj</p>                                                                                                                                                                                                                                                                                                                                        |
| <p><strong>merchant_reference</strong><br>Alphanumeric<br>Mandatory<br>Max: 40</p>  | <p>The Merchant’s unique order number. The merchant reference should be the same for all APIs.<br>Special Characters-_.<br>For example:XYZ9239-yu898</p>                                                                                                                                                                                                                                       |
| <p><strong>language</strong><br>Alpha<br>Mandatory<br>Max:2</p>                     | <p>The checkout page and messages language.Possible</p><p>- en</p><p>- ar</p>                                                                                                                                                                                                                                                                                                                  |
| <p><strong>payment_option</strong><br>Alpha<br>Mandatory<br>Max: 10</p>             | <p>Payment option.<br>For example: VALU</p>                                                                                                                                                                                                                                                                                                                                                    |
| <p><strong>total_downpayment</strong><br>Numeric<br>Optional<br>Max:100</p>         | <p>Defines the total down-payment amount payable by the customer. *Decimal values are not accepted.<br>For example: 1200</p>                                                                                                                                                                                                                                                                   |
| <p><strong>phone_number</strong><br>Alphanumeric<br>Mandatory<br>Max:19</p>         | <p>The customer’s phone number registered for ValU.<br>For example:00008557694</p>                                                                                                                                                                                                                                                                                                             |
| <p><strong>amount</strong><br>Numeric<br>Mandatory<br>Max:10</p>                    | <p>The transaction’s amount. *Each currency has predefined allowed decimal points that should be taken into consideration when sending the amount.<br>For example:10000</p>                                                                                                                                                                                                                    |
| <p><strong>currency</strong><br>Alpha<br>Mandatory<br>Max: 3</p>                    | The currency of the transaction amount in ISO code 3. For example: EGP                                                                                                                                                                                                                                                                                                                         |
| <p><strong>signature</strong><br>Alphanumeric<br>Mandatory<br>Max: 200</p>          | <p>A string hashed using the Secure Hash Algorithm. Please refer to section <a href="broken-reference">Signature</a><br><br>For example 7cad05f0212ed933c9a5d5dffa31661acf2c827a</p>                                                                                                                                                                                                           |
| <p><strong>wallet_amount</strong><br>Numeric<br>Mandatory<br>Max:10</p>             | <p>Wallet amount or ToU is a gift balance that you can purchase using your valU limit and can pay in flexible installment plans from 6-60 months. You can transfer ToU balance to all of your loved ones, they don’t need to be valU customers. *Each currency has predefined allowed decimal points that should be taken into consideration when sending the amount.<br>For example:10000</p> |
| <p><strong>cashback_wallet_amount</strong><br>Numeric<br>Mandatory<br>Max:10</p>    | <p>Amount stored in cashback wallet. *Each currency has predefined allowed decimal points that should be taken into consideration when sending the amount.<br>For example:10000</p>                                                                                                                                                                                                            |

## Get Installment Plans Response

> Response Example

| Parameter Name                                                                   | Description                                                                                                                                                                                                                                                                                                                                                                                    |
| -------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>service_command</strong><br>Alpha<br>Max: 20</p>                      | <p>Command.<br>Possible Values: GET_INSTALLMENTS_PLANS</p>                                                                                                                                                                                                                                                                                                                                     |
| <p><strong>access_code</strong><br>Alphanumeric<br>Max: 20</p>                   | <p>Access code.<br>For example: Lzx0IPmPy5 jp1vAz8Kpg7</p>                                                                                                                                                                                                                                                                                                                                     |
| <p><strong>merchant_identifier</strong><br>Alphanumeric<br>Max:20</p>            | <p>The ID of the Merchant.<br>For example:CycHZxVj</p>                                                                                                                                                                                                                                                                                                                                         |
| <p><strong>merchant_reference</strong><br>Alphanumeric<br>Max: 40</p>            | <p>The Merchant’s unique order number. The merchant reference should be the same for all APIs.<br>Special Characters-_=.<br>XYZ9239-yu898</p>                                                                                                                                                                                                                                                  |
| <p><strong>language</strong><br>Alpha<br>Max: 2</p>                              | <p>The checkout page and messages language. For example<br>- en<br>- ar</p>                                                                                                                                                                                                                                                                                                                    |
| <p><strong>payment_option</strong><br>Alpha<br>Max: 10</p>                       | <p>Payment option.<br>For example</p><p>VALU</p>                                                                                                                                                                                                                                                                                                                                               |
| <p><strong>total_downpayment</strong><br>Numeric<br>Max: 100</p>                 | <p>Defines the total down-payment amount payable by the customer. *Decimal values are not accepted.<br>Special Characters -<br>For example: 1200</p>                                                                                                                                                                                                                                           |
| <p><strong>phone_number</strong><br>Alphanumeric<br>Max: 19</p>                  | <p>The customer’s phone number registered for ValU.<br>00008557694</p>                                                                                                                                                                                                                                                                                                                         |
| <p><strong>amount</strong><br>Numeric<br>Max:10</p>                              | <p>The transaction’s amount. *Each currency has predefined allowed decimal points that should be taken into consideration when sending the amount.<br>For example: 10000</p>                                                                                                                                                                                                                   |
| <p><strong>currency</strong><br>Alpha<br>Max: 3</p>                              | <p>The currency of the transaction amount in ISO code 3.<br>For example: EGP</p>                                                                                                                                                                                                                                                                                                               |
| <p><strong>signature</strong><br>Alphanumeric<br>Max: 200</p>                    | <p>A string hashed using the Secure Hash Algorithm.Please refer to section <a href="broken-reference">Signature</a><br></p>                                                                                                                                                                                                                                                                    |
| <p><strong>installment_detail</strong><br>List</p>                               | A list of all the details of installments, such as number of installments, fees due every month.                                                                                                                                                                                                                                                                                               |
| <p><strong>wallet_amount</strong><br>Numeric<br>Mandatory<br>Max:10</p>          | <p>Wallet amount or ToU is a gift balance that you can purchase using your valU limit and can pay in flexible installment plans from 6-60 months. You can transfer ToU balance to all of your loved ones, they don’t need to be valU customers. *Each currency has predefined allowed decimal points that should be taken into consideration when sending the amount.<br>For example:10000</p> |
| <p><strong>cashback_wallet_amount</strong><br>Numeric<br>Mandatory<br>Max:10</p> | <p>Amount stored in cashback wallet. *Each currency has predefined allowed decimal points that should be taken into consideration when sending the amount.<br>For example:10000</p>                                                                                                                                                                                                            |

## Customer Verify

This request allows the Merchant to identify whether the customer is a ValU registered customer or not; by verifying the Customer’s phone number.

### Customer Verify – Request

> Customer Verify Request Example

```json
{

"service_command":"CUSTOMER_VERIFY", "merchant_reference":"XYZ9239-yu898", "merchant_identifier":"CycHZxVj", "access_code":"zx0IPmPy5jp1vAz8Kpg7", "language":"en",
"payment_option":"VALU",

"phone_number":"00008557694",

"signature":"54efbd76bd644e9ef237c39137bf5d2304dc1bfdf6f6302065b448f2456a07a7"

}
```

**Customer Verify Request Parameters**

```shell
 {

"service_command":"CUSTOMER_VERIFY", "merchant_reference":"XYZ9239-yu898", "merchant_identifier":"CycHZxVj", "access_code":"zx0IPmPy5jp1vAz8Kpg7", "language":"en",
"payment_option":"VALU",

"phone_number":"00008557694",

"signature":"54efbd76bd644e9ef237c39137bf5d2304dc1bfdf6f6302065b448f2456a07a7"

}
```

```php
error_reporting(E_ALL);
ini_set('display_errors', '1');

$url = 'https://sbpaymentservices.payfort.com/FortAPI/paymentApi';
$arrData = array(
   'service_command'=>'CUSTOMER_VERIFY', 'merchant_reference'=>'XYZ9239-yu898', 'merchant_identifier'=>'CycHZxVj', 'access_code'=>'zx0IPmPy5jp1vAz8Kpg7', 'language'=>'en',
'payment_option'=>'VALU',

'phone_number'=>'00008557694',

'signature'=>'54efbd76bd644e9ef237c39137bf5d2304dc1bfdf6f6302065b448f2456a07a7'
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
    'service_command':'CUSTOMER_VERIFY', 'merchant_reference':'XYZ9239-yu898', 'merchant_identifier':'CycHZxVj', 'access_code':'zx0IPmPy5jp1vAz8Kpg7', 'language':'en',
'payment_option':'VALU',

'phone_number':'00008557694',

'signature':'54efbd76bd644e9ef237c39137bf5d2304dc1bfdf6f6302065b448f2456a07a7'
    
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
arrData = {
    'service_command'=>'CUSTOMER_VERIFY', 'merchant_reference'=>'XYZ9239-yu898', 'merchant_identifier'=>'CycHZxVj', 'access_code'=>'zx0IPmPy5jp1vAz8Kpg7', 'language'=>'en',
'payment_option'=>'VALU',

'phone_number'=>'00008557694',

'signature'=>'54efbd76bd644e9ef237c39137bf5d2304dc1bfdf6f6302065b448f2456a07a7'
};


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
String jsonRequestString = "{\n\n\"service_command\":\"CUSTOMER_VERIFY\", \"merchant_reference\":\"XYZ9239-yu898\", \"merchant_identifier\":\"CycHZxVj\", \"access_code\":\"zx0IPmPy5jp1vAz8Kpg7\", \"language\":\"en\",\n\"payment_option\":\"VALU\",\n\n\"phone_number\":\"00008557694\",\n\n\"signature\":\"54efbd76bd644e9ef237c39137bf5d2304dc1bfdf6f6302065b448f2456a07a7\"\n\n}";

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

| Parameter Name                                                                      | Description                                                                                                                                                              |
| ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <p><strong>service_command</strong><br>Alpha<br>Max: 20<br>Mandatory</p>            | <p>Command<br>For example:CUSTOMER_VERIFY</p>                                                                                                                            |
| <p><strong>access_code</strong><br>Alphanumeric<br>Mandatory<br>Max:20</p>          | <p>Access code.<br>For example:zx0IPmPy5jp1vAz8Kpg7</p>                                                                                                                  |
| <p><strong>merchant_identifier</strong><br>Alphanumeric<br>Mandatory<br>Max: 20</p> | <p>The ID of the Merchant.<br>For example:CycHZxVj</p>                                                                                                                   |
| <p><strong>merchant_reference</strong><br>Alphanumeric<br>Mandatory<br>Max:40</p>   | <p>The Merchant’s unique order number. The merchant reference should be the same for all APIs.<br>Special Characters:-_.<br>For example: XYZ9239-yu898</p>               |
| <p><strong>language</strong><br>Alpha<br>Mandatory<br>Max: 2</p>                    | The checkout page and messages language.                                                                                                                                 |
| <p><strong>payment_option</strong><br>Alpha<br>Mandatory<br>Max: 10</p>             | <p>Payment option.<br>For example:VALU</p>                                                                                                                               |
| <p><strong>phone_number</strong><br>Alphanumeric<br>Mandatory<br>Max:19</p>         | <p>The customer’s phone number registered for ValU.<br>For example: 00008557694</p>                                                                                      |
| <p><strong>signature</strong><br>Alphanumeric<br>Mandatory<br>Max: 200</p>          | <p>A string hashed using the Secure Hash Algorithm. Please refer to section <a href="broken-reference">Signature</a><br><br>7cad05f0212ed933c9a5d5dffa31661acf2c827a</p> |

### Customer Verify – Response

**Customer Verify Response Parameters**

| Parameter Name                                                         | Description                                                                                                                                                                                                                             |
| ---------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>service_command</strong><br>Alpha<br>Max: 20</p>            | <p>Command.<br>For example: CUSTOMER_VERIFY</p>                                                                                                                                                                                         |
| <p><strong>access_code</strong><br>Alphanumeric<br>Max:20</p>          | <p>Access code.<br>For example:zx0IPmPy5jp1vAz8Kpg7</p>                                                                                                                                                                                 |
| <p><strong>merchant_identifier</strong><br>Alphanumeric<br>Max: 20</p> | <p>The ID of the Merchant.<br>For example: CycHZxVj</p>                                                                                                                                                                                 |
| <p><strong>merchant_reference</strong><br>Alphanumeric<br>Max: 40</p>  | <p>The Merchant’s unique order number. The merchant reference should be the same for all APIs.<br>Special Characters: -_.<br>For example: XYZ9239-yu898</p>                                                                             |
| <p><strong>language</strong><br>Alpha<br>Max: 2</p>                    | <p>The checkout page and messages language.<br>For example<br>- en<br>- ar</p>                                                                                                                                                          |
| <p><strong>payment_option</strong><br>Alpha<br>Max:10</p>              | <p>Payment option.For example</p><p>VALU</p>                                                                                                                                                                                            |
| <p><strong>total_downpayment</strong><br>Numeric<br>Max: 100</p>       | <p>Defines the total down-payment amount payable by the customer. *Decimal values are not accepted.<br>For example: 1200</p>                                                                                                            |
| <p><strong>phone_number</strong><br>Alphanumeric<br>Max: 19</p>        | <p>The customer’s phone number registered for ValU.<br>For example:00008557694</p>                                                                                                                                                      |
| <p><strong>amount</strong><br>Numeric<br>Max: 10</p>                   | <p>The transaction’s amount. *Each currency has predefined allowed decimal points that should be taken into consideration when sending the amount.<br>Max: 10000</p>                                                                    |
| <p><strong>currency</strong><br>Alpha<br>Max: 3</p>                    | <p>The currency of the transaction amount in ISO code 3.<br>For example: EGP</p>                                                                                                                                                        |
| <p><strong>signature</strong><br>Alphanumeric<br>Max: 200</p>          | <p>A string hashed using the Secure Hash Algorithm. Please refer to section <a href="broken-reference">Signature</a><br><br>For example: aa7cad05f0212ed933c9a5d5dffa31661acf2c827a</p>                                                 |
| <p><strong>response_message</strong><br>Alphanumeric<br>Max: 150</p>   | Message description of the response code. It returns according to the request language.Please refer to section [messages](broken-reference)                                                                                             |
| <p><strong>response_code</strong><br>Numeric<br>Max:5</p>              | <p>Response code carries the value of our system's response.</p><p>*The code consists of five digits, the first 2 digits represent the response status, and the last 3 digits represent the response message.<br>For example: 88000</p> |
| <p><strong>status</strong><br>Numeric<br>Max: 2</p>                    | A two-digit numeric value that indicates the status of the transaction.Please refer to section [statuses](broken-reference)                                                                                                             |

Was this helpful? Yes NoThank you for helping improve Amazon Payment Services' documentation. If you need help or have any questions,Get In Touchor contact us on integration-ps@amazon.com.
