
#Inbound 

The Inbound APIs will be used by sending partners to integrate with TerraPay to send transaction requests.

### View Account Status 


The Accounts Status API validates the status of the beneficiary  bank account and also matches the name of the beneficiary provided by the sender with the name of the beneficiary registered on the financial instrument. This service is available only in corridors where the receiving partner provides details of the beneficiary account such as the account state and beneficiary name. In cases where this information is not available TerraPay does basic validation on the mobile number and bank account format. The status enables the client to determine whether transactions can be subsequently sent to the beneficiary account. 

**URI format is:** https://uat-connect.terrapay.com:21211/eig/gsma/accounts/{AccountIdentifiers}/status

### View Account Status of a Mobile Wallet  <a class="tryitbutton" href='https://developers.terrapay.com/try-it/account-status-mobile' target="_blank">Try it </a>



>View Account Status of a Mobile Wallet

```shell-screen-1
curl --location --request GET 'https://uat-connect.terrapay.com:21211/eig/gsma/accounts/msisdn/+9779840002320/status?bnv=David Robinson' \
--header 'X-USERNAME: terrapayuser' \
--header 'X-PASSWORD:101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b' \
--header 'X-DATE: 2017-05-03 11:00:00' \
--header 'X-ORIGINCOUNTRY: US'
```

```javascript-screen-1
var myHeaders = new Headers();
myHeaders.append("X-USERNAME", "terrapayuser");
myHeaders.append("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b");
myHeaders.append("X-DATE", "2018-04-04 09:27:16");
myHeaders.append("X-ORIGINCOUNTRY", "US");

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  redirect: 'follow'
};

fetch("https://uat-connect.terrapay.com:21211/eig/gsma/accounts/msisdn/+9779840002320/status?bnv=David Robinson", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```


```python-screen-1
import requests

url = "https://uat-connect.terrapay.com:21211/eig/gsma/accounts/msisdn/+9779840002320/status?bnv=David Robinson"

payload={}
headers = {
  'X-USERNAME': 'terrapayuser',
  'X-PASSWORD': '101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b',
  'X-DATE': '2018-04-04 09:27:16',
  'X-ORIGINCOUNTRY': 'US'
}

response = requests.request(""GET"", url, headers=headers, data=payload)

print(response.text)

```
```java-screen-1
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
Request request = new Request.Builder()
  .url("https://uat-connect.terrapay.com:21211/eig/gsma/accounts/msisdn/+9779840002320/status?bnv=David Robinson")
  .method("GET", null)
  .addHeader("X-USERNAME", "terrapayuser")
  .addHeader("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b
")
  .addHeader("X-DATE", "2018-04-04 09:27:16")
  .addHeader("X-ORIGINCOUNTRY", "US")
  .build();
Response response = client.newCall(request).execute();
```
```ruby-screen-1
require "uri"
require "net/http"

url = URI("https://uat-connect.terrapay.com:21211/eig/gsma/accounts/msisdn/+9779840002320/status?bnv=David Robinson")

https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true

request = Net::HTTP::Get.new(url)
request["X-USERNAME"] = "terrapayuser"
request["X-PASSWORD"] = "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b
"
request["X-DATE"] = "2018-04-04 09:27:16"
request["X-ORIGINCOUNTRY"] = "US"

response = https.request(request)
puts response.read_body

```


> Success Response: 

```json
{
	"status":"available", 
	"subStatus":"6000:Beneficiary MSISDN Validation Success", 
	"lei":""
}
```

> Failure Response : 

```json
{
	"error": 
	{
		"errorCategory":"authorisation", 
		"errorCode":"1003", 
		"errorDescription":"Authentication failed. Username or Password is incorrect.", 
		"errorDateTime":"2017-05-02 11:00:00"
	}
}
```

```json
{
	"error": 
	{
		"errorCategory":"businessRule", 
		"errorCode":"6008", 
		"errorDescription":"Beneficiary name does not match", 
		"errorDateTime":"2017-05-02 11:00:00"
	}
}
```
### URL 
https://uat-connect.terrapay.com:21211/eig/gsma/accounts/msisdn/{msisdn}/status?bnv={beneficiaryName}&provider={provider}&snv={senderName}

### HTTP Request
`GET /eig/gsma/accounts/msisdn/+234xxxxxxxxx/status?bnv=John%20Smith&provider=23401&snv=David%20Robinson HTTP/1.1`

### Request Parameters
Parameter | Description |Data type |Requirement | Field Length |
--------- | ----------- |----------|----------- | ----------- |
msisdn|Beneficiary MSISDN with country code. This corresponds to the mobile wallet to which funds are to be transferred. Eg. +91xxxxxxxxxx|String|Mandatory|10-18
bnv|Full KYC name of the beneficiary as registered with the wallet provider.|String|	Mandatory|	1-50
snv | Full name of the sender as per KYC Id document.	| String | Optional | 1-50
provider|This is a code which indicates the mobile operator network to which the transaction is to be sent. This field is conditional. If not set, TerraPay will automatically find the mobile network that the beneficiary MSISDN belongs to and will validate the MSISDN. If set, then TerraPay will validate the MSISDN against the mobile network specified. In case the provider code does not match the mobile network the validation will be rejected.<aside class="success">**NOTE**: Mandatory for wallet transactions to China, Bangladesh, Indonesia, Nepal, Pakistan, Philippines, South Sudan, Togo, Vietnam, Cambodia, Columbia & Haiti.  Optional for other countries. </aside>| Numeric| Conditional	|5


### View Account Status of a Bank Account <a class="tryitbutton" href='https://developers.terrapay.com/try-it/account-status-bank' target="_blank">Try it </a>


> View Account Status of a Bank Account

```shell-screen-2
curl --location --request GET 'https://uat-connect.terrapay.com:21211/eig/gsma/accounts/232201001617/status?bnv=Devki%20Luggage%20Centre&bankname=Canara%20Bank&country=IN&bankcode=CNRB0000232' \

--header 'X-USERNAME: terrapayuser' \
--header 'X-PASSWORD: 101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b' \
--header 'X-DATE: 2020-01-02 10:51:16' \
--header 'X-ORIGINCOUNTRY: US' \
--header 'Content-Type: application/json'
```

```javascript-screen-2
var myHeaders = new Headers();
myHeaders.append("X-USERNAME", "terrapayuser");
myHeaders.append("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b");
myHeaders.append("X-DATE", "2018-04-04 09:27:16");
myHeaders.append("X-ORIGINCOUNTRY", "US");

var raw = "";

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("https://uat-connect.terrapay.com:21211/eig/gsma/accounts/50100002965304/status?bnv=Deepa%20Jain&bankcode=HDFC0001626&bankname=HDFC%20Bank&country=IN", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```python-screen-2
import requests

url = "https://uat-connect.terrapay.com:21211/eig/gsma/accounts/50100002965304/status?bnv=Deepa%20Jain&bankcode=HDFC0001626&bankname=HDFC%20Bank&country=IN"

payload = ""
headers = {
  'X-USERNAME': 'terrapayuser',
  'X-PASSWORD': '101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b',
  'X-DATE': '2018-04-04 09:27:16',
  'X-ORIGINCOUNTRY': 'US'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)

```

```java-screen-2
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
Request request = new Request.Builder()
  .url("https://uat-connect.terrapay.com:21211/eig/gsma/accounts/50100002965304/status?bnv=Deepa%20Jain&bankcode=HDFC0001626&bankname=HDFC%20Bank&country=IN")
  .method("GET", null)
  .addHeader("X-USERNAME", "terrapayuser")
  .addHeader("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b")
  .addHeader("X-DATE", "2018-04-04 09:27:16")
  .addHeader("X-ORIGINCOUNTRY", "US")
  .build();
Response response = client.newCall(request).execute();
````

```ruby-screen-2
require "uri"
require "net/http"

url = URI("https://uat-connect.terrapay.com:21211/eig/gsma/accounts/50100002965304/status?bnv=Deepa%20Jain&bankcode=HDFC0001626&bankname=HDFC%20Bank&country=IN")

https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true

request = Net::HTTP::Get.new(url)
request["X-USERNAME"] = "terrapayuser"
request["X-PASSWORD"] = "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b"
request["X-DATE"] = "2018-04-04 09:27:16"
request["X-ORIGINCOUNTRY"] = "US"

response = https.request(request)
puts response.read_body

```


> Success Response: 


```json
{
	"status":"available", 
	"subStatus":"6000:Beneficiary Bank Account Validation Success", 
	"lei":""
}
```

> Failure Response : 

```json
{
	"error": 
	{
		"errorCategory":"authorisation", 
		"errorCode":"1003", 
		"errorDescription":"Authentication failed. Username or Password is incorrect.", 
		"errorDateTime":"2017-05-02 11:00:00"
	}
}

```

```json
{
	"error": 
	{
		"errorCategory":"businessRule", 
		"errorCode":"6008", 
		"errorDescription":"Beneficiary name does not match", 
		"errorDateTime":"2017-05-02 11:00:00"
	}
}
```
### URL
https://uat-connect.terrapay.com:21211/eig/gsma/accounts/{accountId}/status?bnv={beneficiaryName}&bankcode={bankCode}&bankname={bankName}&country={countryCode}&msisdn={msisdn}&provider={provider}&snv={senderName}&banksubcode={banksubcode}

### HTTP Request

`GET /eig/gsma/accounts/232698745623/status?bnv=John%20Smith&bankcode=CBKEKENX&bankname=CENTRAL%20BANK%20OF%20KENYA&country=US&provider=2549008&snv=David%20Robinson HTTP/1.1`

### Request Parameters
Parameter | Description |Data type |Requirement | Field Length |
--------- | ----------- |----------|----------- | ----------- |
accountId | Beneficiary Bank Account or IBAN Number as applicable in the destination country for receiving funds. Eg. 2365417895.| String | Mandatory | 5-50
bnv | Full KYC name of the beneficiary as registered with the bank. | String | Mandatory | 1-50
snv | Full name of the sender as per KYC Id document.	| String | Optional | 1-50
bankcode | Bank Code as required in the destination Country. It can be one of IFSC Code , Routing Code, Swift BIC . This code is specific to bank integration in each country and may be mandatory in certain destination countries | String | Conditional | 4-25
bankname | Full name of the beneficiary bank | String | Mandatory | 4-60
country | ISO Alpha 2 country code of the destination country. Eg. NG for Nigeria | String | Mandatory | 2
msisdn | Beneficiary mobile number with country code in countries where is it mandatory for bank transfers. Eg. +91xxxxxxxxxx <aside class="success">**NOTE**: Mandatory for Vietnam termination. Optional for other countries.</aside> | String | Conditional | 10-18
provider | This is a code that indicates the bank to which the transaction is to be sent.This field is conditional. If not set, then TerraPay will resolve the bank based on the bankCode. If the bankCode is incorrectly provided, then the bank will be resolved based on Bank Name (should match exactly as per the bank list shared by TerraPay). If these parameters do no match then the transaction will be rejected. If set, then TerraPay will resolve the bank based on the provider code.<aside class="success">**NOTE**:Mandatory for bank transactions to Bangladesh & China.Mandatory provider code for China Union Pay is CNUNIONPAY. Mandatory provider code for Philippines Direct to bank transfer is PH_DIRECT_TO_BANK.Optional for other countries. </aside> | Numeric | Conditional | 7-12
banksubcode | This is a code that indicates the branch code of the specific bank to which the transaction is to be sent.<aside class="success">**NOTE**: Mandatory for bank transactions to Brazil & Uruguay.If the transaction is to Bangladesh then partner can send rounting number in banksubcode and they do not have to send the provider code.Optional for other countries.</aside> | String | Conditional |5

### Response Parameters

 Parameter | Description |Data type | Validation |
 --------- | ----------- |----------|----------- | 
 status | Indicates the status of the account. If 'available' then the account can receive funds. If not then transactions sent to the account will fail.	| String | Enumeration = available, unavailable, unregistered
 subStatus | Property can be used to return a provider-specific status for the account.	|String
 lei | Indicates the Legal Entity Identifier of the organization holding the account. | String | Length = 20, Regular Expression


## Create a Quotation 

The quotations API is used to obtain the foreign exchange rate between a currency pair. 

**URI format is:** /quotations
### Create a Quotation to Mobile Wallet <a class="tryitbutton" href='https://developers.terrapay.com/try-it/create-quotation-mobile' target="_blank">Try it </a>


> Create a Quotation to Mobile Wallet

```shell-screen-3
curl --location --request POST 'https://127.0.0.1:21211/eig/gsma/quotations' \
--header 'X-DATE: 2020-01-02 10:51:16' \
--header 'X-ORIGINCOUNTRY: US' \
--header 'X-USERNAME: terrapayuser' \
--header 'X-PASSWORD: 101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b' \
--header 'Content-Type: application/json' \
--data-raw '{
"requestDate": "2020-01-02 10:51:16",
   "debitParty": [
    {
      "key": "msisdn",
      "value": "+4491509874561"
      
    }
  ],
   "creditParty": [
    {
      "key": "msisdn",
      "value": "+256897378380"
    }
  ],
  "requestAmount": "100",
  "requestCurrency": "USD",
   "quotes": [
    {
      "sendingCurrency": "USD",
      "receivingCurrency": "UGX"
    }
  ]
 }
```

```javascript-screen-3
var myHeaders = new Headers();
myHeaders.append("X-USERNAME", "terrapayuser");
myHeaders.append("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b");
myHeaders.append("X-DATE", "2018-04-04 09:27:16");
myHeaders.append("X-ORIGINCOUNTRY", "US");
myHeaders.append("Content-Type", "application/json");

var raw = JSON.stringify({
  "requestDate": "2017-06-20 12:27:16",
  "creditParty": [
    {
      "key": "msisdn",
      "value": "+9779840002320"
    }
  ],
  "requestAmount": "500",
  "requestCurrency": "NPR",
  "quotes": [
    {
      "sendingCurrency": "USD",
      "receivingCurrency": "NPR"
    }
  ]
});

var requestOptions = {
  method: 'POST',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("https://uat-connect.terrapay.com:21211/eig/gsma/quotations", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```


```python-screen-3
import requests
import json

url = "https://uat-connect.terrapay.com:21211/eig/gsma/quotations"

payload = json.dumps({
  "requestDate": "2017-06-20 12:27:16",
  "creditParty": [
    {
      "key": "msisdn",
      "value": "+9779840002320"
    }
  ],
  "requestAmount": "500",
  "requestCurrency": "NPR",
  "quotes": [
    {
      "sendingCurrency": "USD",
      "receivingCurrency": "NPR"
    }
  ]
})
headers = {
  'X-USERNAME': 'terrapayuser',
  'X-PASSWORD': '101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b',
  'X-DATE': '2018-04-04 09:27:16',
  'X-ORIGINCOUNTRY': 'US',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```java-screen-3
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, "{\r\n    \"requestDate\": \"2017-06-20 12:27:16\",\r\n    \"creditParty\": [\r\n        {\r\n            \"key\": \"msisdn\",\r\n            \"value\": \"+9779840002320\"\r\n        }\r\n    ],\r\n    \"requestAmount\": \"500\",\r\n    \"requestCurrency\": \"NPR\",\r\n    \"quotes\": [\r\n        {\r\n            \"sendingCurrency\": \"USD\",\r\n            \"receivingCurrency\": \"NPR\"\r\n        }\r\n    ]\r\n}");
Request request = new Request.Builder()
  .url("https://uat-connect.terrapay.com:21211/eig/gsma/quotations")
  .method("POST", body)
  .addHeader("X-USERNAME", "terrapayuser")
  .addHeader("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b")
  .addHeader("X-DATE", "2018-04-04 09:27:16")
  .addHeader("X-ORIGINCOUNTRY", "US")
  .addHeader("Content-Type", "application/json")
  .build();
Response response = client.newCall(request).execute();
```

```ruby-screen-3
require "uri"
require "json"
require "net/http"

url = URI("https://uat-connect.terrapay.com:21211/eig/gsma/quotations")

https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true

request = Net::HTTP::Post.new(url)
request["X-USERNAME"] = "terrapayuser"
request["X-PASSWORD"] = "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b"
request["X-DATE"] = "2018-04-04 09:27:16"
request["X-ORIGINCOUNTRY"] = "US"
request["Content-Type"] = "application/json"
request.body = JSON.dump({
  "requestDate": "2017-06-20 12:27:16",
  "creditParty": [
    {
      "key": "msisdn",
      "value": "+9779840002320"
    }
  ],
  "requestAmount": "500",
  "requestCurrency": "NPR",
  "quotes": [
    {
      "sendingCurrency": "USD",
      "receivingCurrency": "NPR"
    }
  ]
})

response = https.request(request)
puts response.read_body

```


> Success Response: 

```json
{
	"requestDate": "2017-05-03 11:00:00",
	"debitParty": [
		{
			"key": "msisdn",
			"value": "+4491509874561"
		}
	],
	"creditParty": [
		{
			"key": "msisdn",
			"value": "+25691508523697"
		}
	],
	"requestAmount": "100",
	"requestCurrency": "EUR",
	"quotes": [
		{
			"quoteId": "QT037fQXs3LGWXea4",
			"quoteExpiryTime": "2017-05-03 11:28:00",
			"sendingAmount": "100.000000",
			"sendingCurrency": "EUR",
			"receivingAmount": "365217",
			"receivingCurrency": "UGX",
			"fxRate": "3652.173913"
		}
	],
	"quotationReference": "QT037fQXs3LGWXea4",
	"quotationStatus": "2000:Quote Success"
}
```

> Failure Response : 

```json
{
	"error": {
		"errorCategory":"authorisation", 
		"errorCode":"1003", 
		"errorDescription":"Authentication failed. Username or Password is incorrect.",
		"errorDateTime":"2017-05-02 11:00:00" 
	}
}
```

```json
{
	"error": {
    	"errorCategory":"businessRule", 
    	"errorCode":"2001", 
    	"errorDescription":"Source amount is invalid",
    	"errorDateTime":"2017-05-02 11:00:00" 
 	}
}
```

```json
{
	"error": {
		"errorCategory":"businessRule", 
    	"errorCode":"2003", 
    	"errorDescription":"Failed to get Forex rate",
    	"errorDateTime":"2017-05-02 11:00:00" 
	}
}
```
### URL
https://uat-connect.terrapay.com:21211/eig/gsma/quotations
### HTTP Request
`POST /eig/gsma/quotations HTTP/1.1`

### Create a Quotation to Bank Account <a class="tryitbutton" href='https://developers.terrapay.com/try-it/create-quotation-bank' target="_blank">Try it </a>


> Create a Quotation to Bank Account

```shell-screen-4
curl --location --request POST 'https://uat-connect.terrapay.com:21211/eig/gsma/quotations'\
--header 'X-DATE: 2020-01-02 10:51:16'\
--header 'X-ORIGINCOUNTRY: US' \
--header 'X-USERNAME: terrapayuser' \
--header 'X-PASSWORD:   101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b' \
--header 'Content-Type: application/json' \
--data-raw '{
  "requestDate": "2017-05-03 11:00:00",
	"debitParty": [
		{
			"key": "msisdn",
			"value": "+4491509874561"
		}
	],
	"creditParty": [
		{
			"key": "msisdn",
			"value": "+25691508523697"
		},
		{
			"key": "bankaccountno",
			"value": "2356915085237"
		},
		{
			"key": "receivingCountry",
			"value": "NG"
		}
	],
	"requestAmount": "100",
	"requestCurrency": "EUR",
	"quotes": [
		{
			"sendingCurrency": "EUR",
			"receivingCurrency": "UGX"
		}
	]    
}
```
```javascript-screen-4
var myHeaders = new Headers();
myHeaders.append("X-USERNAME", "terrapayuser");
myHeaders.append("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b");
myHeaders.append("X-DATE", "2018-04-04 09:27:16");
myHeaders.append("X-ORIGINCOUNTRY", "US");
myHeaders.append("Content-Type", "application/json");

var raw = JSON.stringify({
  "requestDate": "2017-06-20 12:27:16",
  "creditParty": [
    {
      "key": "bankaccountno",
      "value": "50100002965304"
    },
    {
      "key": "receivingCountry",
      "value": "IN"
    }
  ],
  "requestAmount": "500",
  "requestCurrency": "INR",
  "quotes": [
    {
      "sendingCurrency": "USD",
      "receivingCurrency": "INR"
    }
  ]
});

var requestOptions = {
  method: 'POST',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("https://uat-connect.terrapay.com:21211/eig/gsma/quotations", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```
```python-screen-4
import requests
import json

url = "https://uat-connect.terrapay.com:21211/eig/gsma/quotations"

payload = json.dumps({
  "requestDate": "2017-06-20 12:27:16",
  "creditParty": [
    {
      "key": "bankaccountno",
      "value": "50100002965304"
    },
    {
      "key": "receivingCountry",
      "value": "IN"
    }
  ],
  "requestAmount": "500",
  "requestCurrency": "INR",
  "quotes": [
    {
      "sendingCurrency": "USD",
      "receivingCurrency": "INR"
    }
  ]
})
headers = {
  'X-USERNAME': 'terrapayuser',
  'X-PASSWORD': '101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b',
  'X-DATE': '2018-04-04 09:27:16',
  'X-ORIGINCOUNTRY': 'US',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```java-screen-4
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, "{\r\n    \"requestDate\": \"2017-06-20 12:27:16\",\r\n    \"creditParty\": [\r\n        {\r\n\t\t  \"key\": \"bankaccountno\",\r\n\t\t  \"value\": \"50100002965304\"\r\n\t\t},\r\n\t\t{\r\n\t\t\t\"key\": \"receivingCountry\",\r\n\t\t\t\"value\": \"IN\"\r\n\t\t}\r\n    ],\r\n    \"requestAmount\": \"500\",\r\n    \"requestCurrency\": \"INR\",\r\n    \"quotes\": [\r\n        {\r\n            \"sendingCurrency\": \"USD\",\r\n            \"receivingCurrency\": \"INR\"\r\n        }\r\n    ]\r\n}");
Request request = new Request.Builder()
  .url("https://uat-connect.terrapay.com:21211/eig/gsma/quotations")
  .method("POST", body)
  .addHeader("X-USERNAME", "terrapayuser")
  .addHeader("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b")
  .addHeader("X-DATE", "2018-04-04 09:27:16")
  .addHeader("X-ORIGINCOUNTRY", "US")
  .addHeader("Content-Type", "application/json")
  .build();
Response response = client.newCall(request).execute();
```
```ruby-screen-4
require "uri"
require "json"
require "net/http"

url = URI("https://uat-connect.terrapay.com:21211/eig/gsma/quotations")

https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true

request = Net::HTTP::Post.new(url)
request["X-USERNAME"] = "terrapayuser"
request["X-PASSWORD"] = "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b"
request["X-DATE"] = "2018-04-04 09:27:16"
request["X-ORIGINCOUNTRY"] = "US"
request["Content-Type"] = "application/json"
request.body = JSON.dump({
  "requestDate": "2017-06-20 12:27:16",
  "creditParty": [
    {
      "key": "bankaccountno",
      "value": "50100002965304"
    },
    {
      "key": "receivingCountry",
      "value": "IN"
    }
  ],
  "requestAmount": "500",
  "requestCurrency": "INR",
  "quotes": [
    {
      "sendingCurrency": "USD",
      "receivingCurrency": "INR"
    }
  ]
})

response = https.request(request)
puts response.read_body

```



> Success Response: 

```json
{
	"requestDate": "2017-05-03 11:00:00",
	"debitParty": [
		{
			"key": "msisdn",
			"value": "+4491509874561"
		}
	],
	"creditParty": [
		{
			"key": "msisdn",
			"value": "+25691508523697"
    	},
    	{
      		"key": "bankaccountno",
      		"value": "2356915085237"
    	},
   		{
     		"key": "receivingCountry",
      		"value": "NG"
    	}
  	],
  	"requestAmount": "100",
  	"requestCurrency": "EUR",
  	"quotes": [
   		{
			"quoteId": "QT037fQXs3LGWXea4",
			"quoteExpiryTime": "2017-05-03 11:28:00",
			"sendingAmount": "100.000000",
			"sendingCurrency": "EUR",
			"receivingAmount": "365217",
			"receivingCurrency": "UGX",
			"fxRate": "3652.173913"
		}
	],
	"quotationReference": "QT037fQXs3LGWXea4",
	"quotationStatus": "2000:Quote Success"
}
```

> Failure Response : 

```json
{
	"error": {
		"errorCategory":"authorisation", 
		"errorCode":"1003", 
		"errorDescription":"Authentication failed. Username or Password is incorrect.",
		"errorDateTime":"2017-05-02 11:00:00"
	}
}
{
	"error": {
		"errorCategory":"businessRule", 
		"errorCode":"2001", 
		"errorDescription":"Source amount is invalid",
		"errorDateTime":"2017-05-02 11:00:00" 
	}
}
{
	"error": {
		"errorCategory":"businessRule", 
		"errorCode":"2003", 
		"errorDescription":"Failed to get Forex rate",
		"errorDateTime":"2017-05-02 11:00:00"
	}
}


```
### URL
https://uat-connect.terrapay.com:21211/eig/gsma/quotations
### HTTP Request
`POST /eig/gsma/quotations HTTP/1.1`

### Request Parameters
Parameter | Description |Data type |Requirement | Field Length |
--------- | ----------- |----------|----------- | ----------- |
requestDate | The creation date and time of the transaction as supplied by the client in YYYY-MM-DD HH:mm:ss | DateTime | Mandatory | 19
requestAmount | Requested quotation amount with precision of 2 decimal places	 | String | Mandatory | 10,2
requestCurrency | Currency of the requestAmount provided in ISO 4217 format. Eg. EUR. If the requestCurrency is the source currency, then the requestAmount is taken as what the sender will pay and the quote is calculated in the destination currency and the quote amount returned will be what the beneficiary will receive. If the requestCurrency is the destination currency, then the requestAmount is taken as what the beneficiary has to receive and the quote is calculated in source currency and the quote amount returned will be what the sender has to pay. (Reverse Quote).	| String | Mandatory | 3
debitParty: |
key | msisdn | String | Optional | 6
value | Sender Mobile Number with country code. Eg.+91xxxxxxxxxx | String | Optional | 10-18
creditParty : |
key | msisdn | String | Conditional | 6
value | Beneficiary Mobile Number with country code. Eg.+91xxxxxxxxxx.| String | Optional - For Bank Accounts Mandatory - For Mobile Wallet | 10-18
key | bankaccountno | String | Conditional | 13
Value |Recieve Bank Account in the destination country for receiving funds. Eg. 2365417895. This key/value pair is optional if the transfer is to a mobile wallet. | String |Mandatory - For Bank Accounts Optional - For Mobile Wallet | 5-50
key | receivingCountry | String | Conditional | 16
Value | Destination Country. Eg. NG. This key/value pair is optional if the transfer is to a mobile wallet.| String |Mandatory - For Bank Accounts Optional - For Mobile Wallet | 5-50
quotes : |
sendingCurrency | Currency of the debitor in ISO 4217 format. Eg. EUR	| String | Mandatory | 3
receivingCurrency | Currency of the creditor in ISO 4217 format. Eg. NGN | String | Mandatory | 3


### Response Parameters

 Parameter | Description |Data Type
 --------- | ----------- |----------
 requestDate | Timestamp as sent by the partner in the request API|String
 requestAmount | Request Amount as sent by the partner in the request API	|String
 requestCurrency | Request currency as sent by the partner in the request API	|String
 debitParty: ||
 key | msisdn|String
 value | Sender Mobile Number as sent by the partner in the request API	|String
 creditParty : ||
 key | msisdn|String
 value | Beneficiary Mobile Number as sent by the partner in the request API|String	
 key | bankaccountno|String
 value | Beneficiary bank account details as sent by the partner in the request API	|String
 key | receivingCountry|String
 value | Destination country as sent by the partner in the request API |String
quotes:	| The quotation object which has the foreign exchange rate and the source and destination amounts. The quotation reference should be used in the transactions as an acceptance of the exchange rate.|
quoteId | The unique ID for this quote provided by the foreign exchange provider.This id will be used by partner as part of transaction request.|String
quoteExpiryTime | The time stamp after which the quote will not be valid. This is in partner local time based on the origin country of transaction|String
sendingAmount | Amount payable by the sender|String	
sendingCurrency | Currency in which the sender will pay the sending amount|String	
receivingAmount | Amount that the beneficiary will receive	|String
receivingCurrency | Currency in which the beneficiary will receive funds	|String
fxRate | Foreign Exchange rate applied on the quote including all markups	|String
quotationReference | TerraPay Quote Reference	|String
quotationStatus | Status of the quotation request. Format is ErrorCode:ErrorMessage	|String


## Create A Transaction 

The Transactions API is used to initiate an international money remittance transaction. 

**URI format is:** /transactions
### Create a transaction to a Mobile Wallet <a class="tryitbutton" href='https://developers.terrapay.com/try-it/create-transaction-mobile' target="_blank">Try it </a>
> Create a transaction to a Mobile Wallet 

```shell-screen-5

curl --location --request POST 'https://127.0.0.1:21211/eig/gsma/transactions' \
--header 'X-DATE: 2020-01-02 10:51:16' \
--header 'X-ORIGINCOUNTRY: US' \
--header 'X-USERNAME: terrapayuser' \
--header 'X-PASSWORD: 101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b' \
--header 'Content-Type: application/json' \
--data-raw 
{
   "amount": "100000.01",
   "currency": "NGN",
   "type": "inttransfer",
   "descriptionText": "Gift for my brother",
   "requestDate": "2017-03-20T06:19:36.969Z",
   "requestingOrganisationTransactionReference": "partnerRefId1234",
   "provider": "23401",
   	"debitParty": [
		{
			"key": "msisdn",
			"value": "+33472034605"
		} 
  	],
	"creditParty": [
		{
			"key": "msisdn",
			"value": "+23410706056"
		}
	],
	"senderKyc": {
		"nationality": "FR",
		"dateOfBirth": "1986-06-28",
		"gender": "M",
		"idDocument": [
			{
				"idType": "nationalidcard",
				"idNumber": "123456789",
				"issueDate": "2003-09-26",
				"expiryDate": "2033-09-26",
				"issuerCountry": "FR"
			}
		],
		"postalAddress": {
			"addressLine1": "49 ",
			"addressLine2": "park street",
			"addressLine3": "walton's road",
			"city": "Lyon",
			"stateProvince": "Lyon",
			"postalCode": "123456",
			"country": "FR"
    	},
		"subjectName": {
			"title": "Mr.",
			"firstName": "Einstein",
			"middleName": "James",
			"lastName": "Bela",
			"fullName": "Einstien James Bela"
		}
	},
	"recipientKyc":{
		"nationality": "FR",
		"dateOfBirth": "1986-06-28",
		"idDocument": [
        	{
				"idType": "nationalidcard",
				"idNumber": "123456789",
				"issueDate": "2003-09-26",
				"expiryDate": "2033-09-26",
				"issuerCountry": "FR"
        	}
		],
		"postalAddress": {
			"addressLine1": "49 ",
			"addressLine2": "park street",
			"addressLine3": "walton's road",
			"city": "Lyon",
			"stateProvince": "Lyon",
			"postalCode": "123456",
			"country": "FR"
		},
		"subjectName": {
			"title": "Mr.",
			"firstName": "Einstein",
			"middleName": "James",
			"lastName": "Bela",
			"fullName": "Einstien James Bela"
		}
	},
	"internationalTransferInformation": {
		"quoteId": "QT037fQXs3LGWXea4",
		"receivingCountry": "NG",
		"remittancePurpose": "Gift",
		"sourceOfFunds": "Salary",
		"relationshipSender": "Brother"
	}
}
```

```javascript-screen-5
var myHeaders = new Headers();
myHeaders.append("X-USERNAME", "terrapayuser");
myHeaders.append("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b");
myHeaders.append("X-DATE", "2018-04-04 09:27:16");
myHeaders.append("X-ORIGINCOUNTRY", "US");
myHeaders.append("Content-Type", "text/plain");

var raw = "{\r\n  \"amount\": \"500\",\r\n  \"currency\": \"NPR\",\r\n  \"type\": \"inttransfer\",\r\n  \"descriptionText\": \"Gift for my brother\",\r\n  \"requestDate\": \"2021-05-23 08:19:36\",\r\n  \"requestingOrganisationTransactionReference\": \"SrcTxnId001\",\r\n  \"debitParty\": [\r\n    {\r\n      \"key\": \"msisdn\",\r\n      \"value\": \"+971810456234\"\r\n    }\r\n  ],\r\n  \"creditParty\": [\r\n    {\r\n      \"key\": \"msisdn\",\r\n      \"value\": \"+9779840002320\"\r\n    }\r\n  ],\r\n  \"senderKyc\": {\r\n    \"nationality\": \"AE\",\r\n    \"dateOfBirth\": \"1967-05-28\",\r\n    \"gender\": \"M\",\r\n    \"idDocument\": [\r\n      {\r\n        \"idType\": \"VOTER_CARD\",\r\n        \"idNumber\": \"13321115521\",\r\n        \"issueDate\": \"1967-05-28\",\r\n        \"expiryDate\": \"2067-05-28\",\r\n        \"issuerCountry\": \"AE\"\r\n      }\r\n    ],\r\n    \"postalAddress\": {\r\n      \"addressLine1\": \"49 , park street\",\r\n      \"addressLine2\": \"12\",\r\n      \"addressLine3\": \"12\",\r\n      \"city\": \"12\",\r\n      \"stateProvince\": \"12\",\r\n      \"postalCode\": \"50000\",\r\n      \"country\": \"US\"\r\n    },\r\n    \"subjectName\": {\r\n      \"firstName\": \"Test\",\r\n      \"middleName\": \"\",\r\n      \"lastName\": \"Sender\",\r\n      \"fullName\": \"Test Sender\"\r\n    }\r\n  },\r\n    \"recipientKyc\": {\r\n    \"subjectName\": {\r\n      \"firstName\": \"David\",\r\n      \"lastName\": \"Robinson\",\r\n      \"fullName\": \"David Robinson\"\r\n    }\r\n  },\r\n  \"internationalTransferInformation\": {\r\n    \"quoteId\": \"QT037C1NQ6BHMV59A3\",\r\n    \"receivingCountry\": \"NP\",\r\n    \"remittancePurpose\": \"Family Maintainance\",\r\n    \"sourceOfFunds\": \"Salary\",\r\n    \"relationshipSender\": \"Brother\"\r\n  }\r\n}";

var requestOptions = {
  method: 'POST',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("https://uat-connect.terrapay.com:21211/eig/gsma/transactions", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```
```python-screen-5
import requests

url = "https://uat-connect.terrapay.com:21211/eig/gsma/transactions"

payload = "{\r\n  \"amount\": \"500\",\r\n  \"currency\": \"NPR\",\r\n  \"type\": \"inttransfer\",\r\n  \"descriptionText\": \"Gift for my brother\",\r\n  \"requestDate\": \"2021-05-23 08:19:36\",\r\n  \"requestingOrganisationTransactionReference\": \"SrcTxnId001\",\r\n  \"debitParty\": [\r\n    {\r\n      \"key\": \"msisdn\",\r\n      \"value\": \"+971810456234\"\r\n    }\r\n  ],\r\n  \"creditParty\": [\r\n    {\r\n      \"key\": \"msisdn\",\r\n      \"value\": \"+9779840002320\"\r\n    }\r\n  ],\r\n  \"senderKyc\": {\r\n    \"nationality\": \"AE\",\r\n    \"dateOfBirth\": \"1967-05-28\",\r\n    \"gender\": \"M\",\r\n    \"idDocument\": [\r\n      {\r\n        \"idType\": \"VOTER_CARD\",\r\n        \"idNumber\": \"13321115521\",\r\n        \"issueDate\": \"1967-05-28\",\r\n        \"expiryDate\": \"2067-05-28\",\r\n        \"issuerCountry\": \"AE\"\r\n      }\r\n    ],\r\n    \"postalAddress\": {\r\n      \"addressLine1\": \"49 , park street\",\r\n      \"addressLine2\": \"12\",\r\n      \"addressLine3\": \"12\",\r\n      \"city\": \"12\",\r\n      \"stateProvince\": \"12\",\r\n      \"postalCode\": \"50000\",\r\n      \"country\": \"US\"\r\n    },\r\n    \"subjectName\": {\r\n      \"firstName\": \"Test\",\r\n      \"middleName\": \"\",\r\n      \"lastName\": \"Sender\",\r\n      \"fullName\": \"Test Sender\"\r\n    }\r\n  },\r\n    \"recipientKyc\": {\r\n    \"subjectName\": {\r\n      \"firstName\": \"David\",\r\n      \"lastName\": \"Robinson\",\r\n      \"fullName\": \"David Robinson\"\r\n    }\r\n  },\r\n  \"internationalTransferInformation\": {\r\n    \"quoteId\": \"QT037C1NQ6BHMV59A3\",\r\n    \"receivingCountry\": \"NP\",\r\n    \"remittancePurpose\": \"Family Maintainance\",\r\n    \"sourceOfFunds\": \"Salary\",\r\n    \"relationshipSender\": \"Brother\"\r\n  }\r\n}"
headers = {
  'X-USERNAME': 'terrapayuser',
  'X-PASSWORD': '101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b',
  'X-DATE': '2018-04-04 09:27:16',
  'X-ORIGINCOUNTRY': 'US',
  'Content-Type': 'text/plain'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```
```java-screen-5
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
MediaType mediaType = MediaType.parse("text/plain");
RequestBody body = RequestBody.create(mediaType, "{\r\n  \"amount\": \"500\",\r\n  \"currency\": \"NPR\",\r\n  \"type\": \"inttransfer\",\r\n  \"descriptionText\": \"Gift for my brother\",\r\n  \"requestDate\": \"2021-05-23 08:19:36\",\r\n  \"requestingOrganisationTransactionReference\": \"SrcTxnId001\",\r\n  \"debitParty\": [\r\n    {\r\n      \"key\": \"msisdn\",\r\n      \"value\": \"+971810456234\"\r\n    }\r\n  ],\r\n  \"creditParty\": [\r\n    {\r\n      \"key\": \"msisdn\",\r\n      \"value\": \"+9779840002320\"\r\n    }\r\n  ],\r\n  \"senderKyc\": {\r\n    \"nationality\": \"AE\",\r\n    \"dateOfBirth\": \"1967-05-28\",\r\n    \"gender\": \"M\",\r\n    \"idDocument\": [\r\n      {\r\n        \"idType\": \"VOTER_CARD\",\r\n        \"idNumber\": \"13321115521\",\r\n        \"issueDate\": \"1967-05-28\",\r\n        \"expiryDate\": \"2067-05-28\",\r\n        \"issuerCountry\": \"AE\"\r\n      }\r\n    ],\r\n    \"postalAddress\": {\r\n      \"addressLine1\": \"49 , park street\",\r\n      \"addressLine2\": \"12\",\r\n      \"addressLine3\": \"12\",\r\n      \"city\": \"12\",\r\n      \"stateProvince\": \"12\",\r\n      \"postalCode\": \"50000\",\r\n      \"country\": \"US\"\r\n    },\r\n    \"subjectName\": {\r\n      \"firstName\": \"Test\",\r\n      \"middleName\": \"\",\r\n      \"lastName\": \"Sender\",\r\n      \"fullName\": \"Test Sender\"\r\n    }\r\n  },\r\n    \"recipientKyc\": {\r\n    \"subjectName\": {\r\n      \"firstName\": \"David\",\r\n      \"lastName\": \"Robinson\",\r\n      \"fullName\": \"David Robinson\"\r\n    }\r\n  },\r\n  \"internationalTransferInformation\": {\r\n    \"quoteId\": \"QT037C1NQ6BHMV59A3\",\r\n    \"receivingCountry\": \"NP\",\r\n    \"remittancePurpose\": \"Family Maintainance\",\r\n    \"sourceOfFunds\": \"Salary\",\r\n    \"relationshipSender\": \"Brother\"\r\n  }\r\n}");
Request request = new Request.Builder()
  .url("https://uat-connect.terrapay.com:21211/eig/gsma/transactions")
  .method("POST", body)
  .addHeader("X-USERNAME", "terrapayuser")
  .addHeader("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b")
  .addHeader("X-DATE", "2018-04-04 09:27:16")
  .addHeader("X-ORIGINCOUNTRY", "US")
  .addHeader("Content-Type", "text/plain")
  .build();
Response response = client.newCall(request).execute();
```

```ruby-screen-5
require "uri"
require "net/http"

url = URI("https://uat-connect.terrapay.com:21211/eig/gsma/transactions")

https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true

request = Net::HTTP::Post.new(url)
request["X-USERNAME"] = "terrapayuser"
request["X-PASSWORD"] = "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b"
request["X-DATE"] = "2018-04-04 09:27:16"
request["X-ORIGINCOUNTRY"] = "US"
request["Content-Type"] = "text/plain"
request.body = "{\r\n  \"amount\": \"500\",\r\n  \"currency\": \"NPR\",\r\n  \"type\": \"inttransfer\",\r\n  \"descriptionText\": \"Gift for my brother\",\r\n  \"requestDate\": \"2021-05-23 08:19:36\",\r\n  \"requestingOrganisationTransactionReference\": \"SrcTxnId001\",\r\n  \"debitParty\": [\r\n    {\r\n      \"key\": \"msisdn\",\r\n      \"value\": \"+971810456234\"\r\n    }\r\n  ],\r\n  \"creditParty\": [\r\n    {\r\n      \"key\": \"msisdn\",\r\n      \"value\": \"+9779840002320\"\r\n    }\r\n  ],\r\n  \"senderKyc\": {\r\n    \"nationality\": \"AE\",\r\n    \"dateOfBirth\": \"1967-05-28\",\r\n    \"gender\": \"M\",\r\n    \"idDocument\": [\r\n      {\r\n        \"idType\": \"VOTER_CARD\",\r\n        \"idNumber\": \"13321115521\",\r\n        \"issueDate\": \"1967-05-28\",\r\n        \"expiryDate\": \"2067-05-28\",\r\n        \"issuerCountry\": \"AE\"\r\n      }\r\n    ],\r\n    \"postalAddress\": {\r\n      \"addressLine1\": \"49 , park street\",\r\n      \"addressLine2\": \"12\",\r\n      \"addressLine3\": \"12\",\r\n      \"city\": \"12\",\r\n      \"stateProvince\": \"12\",\r\n      \"postalCode\": \"50000\",\r\n      \"country\": \"US\"\r\n    },\r\n    \"subjectName\": {\r\n      \"firstName\": \"Test\",\r\n      \"middleName\": \"\",\r\n      \"lastName\": \"Sender\",\r\n      \"fullName\": \"Test Sender\"\r\n    }\r\n  },\r\n    \"recipientKyc\": {\r\n    \"subjectName\": {\r\n      \"firstName\": \"David\",\r\n      \"lastName\": \"Robinson\",\r\n      \"fullName\": \"David Robinson\"\r\n    }\r\n  },\r\n  \"internationalTransferInformation\": {\r\n    \"quoteId\": \"QT037C1NQ6BHMV59A3\",\r\n    \"receivingCountry\": \"NP\",\r\n    \"remittancePurpose\": \"Family Maintainance\",\r\n    \"sourceOfFunds\": \"Salary\",\r\n    \"relationshipSender\": \"Brother\"\r\n  }\r\n}"

response = https.request(request)
puts response.read_body

````

> Success Response: 

```json
{
	"amount": "100000.01",
	"currency": "NGN",
	"type": "inttransfer",
	"requestDate": "2017-03-20T06:19:36.969Z",
	"requestingOrganisationTransactionReference": "partnerRefId1234",
	"debitParty": [
		{
			"key": "msisdn",
			"value": "+33472034605"
		} 
	],
   "creditParty": [
    	{
       		"key": "msisdn",
       		"value": "+23410706056"
    	}
  	],
    "transactionStatus": "3000:Remit Success",
    "transactionReference": "TPKM000000056269"  
}

```

> Failure Response : 

```json
{
	"serverCorrelationId":"", 
	"clientCorrelationId":"partnerRefId1234",
	"error": {
		"errorCategory":"authorisation", 
		"errorCode":"1003", 
		"errorDescription":"Authentication failed. Username or Password is incorrect.", 
		"errorDateTime":"2017-05-02 11:00:00"
	}
}

```

```json
{
	"serverCorrelationId":"TPKM000000056269", 
	"clientCorrelationId":"partnerRefId1234",
	"error": {
		"errorCategory":"businessRule", 
		"errorCode":"3032", 
		"errorDescription":"Remit Failed.", 
		"errorDateTime":"2017-05-02 11:00:00"
	}
}

```
### URL
https://uat-connect.terrapay.com:21211/eig/gsma/transactions

### HTTP Request
`POST /eig/gsma/transactions HTTP/1.1`

### Create a transaction to bank <a class="tryitbutton" href='https://developers.terrapay.com/try-it/create-transaction-bank' target="_blank">Try it </a>


> Create a transaction to bank

```shell-screen-6

curl --location --request POST 'https://uat-connect.terrapay.com:21211/eig/gsma/transactions' \
--header 'X-DATE: 2020-01-02 10:51:16' \
--header 'X-ORIGINCOUNTRY: US' \
--header 'X-USERNAME: terrapayuser' \
--header 'X-PASSWORD:101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b' \
--header 'Content-Type: application/json' \
--data-raw 
{
   "amount": "100000.01",
   "currency": "NGN",
   "type": "inttransfer",
   "descriptionText": null,
   "requestDate": "2017-03-20T06:19:36.969Z",
   "requestingOrganisationTransactionReference": "4119314191318",
   	"debitParty": [
		{
			"key": "msisdn",
			"value": "+27123456789"
		}
	],
	"creditParty": [
		{
			"key": "bankaccountno",
			"value": "718530346"
		},
		{
			"key": "sortcode",
			"value": "0001"
		},
		{
			"key": "organisationid",
			"value": "Nu Pagamentos"
		},
		{
			"key": "banksubcode",
			"value": "0001"
		},
		{
			"key": "msisdn",
			"value": "+33472034605"
		}
	],
	"senderKyc": {
		"nationality": "FR",
		"dateOfBirth": "28-06-1986",
		"gender": "M",
		"idDocument": [
			{
				"idType": "nationalidcard",
				"idNumber": "123456789",
				"issueDate": "2003-09-26",
				"expiryDate": "2033-09-26",
				"issuerCountry": "FR"
			}
		],
		"postalAddress": {
			"addressLine1": "49 ",
			"addressLine2": "park street",
			"addressLine3": "walton's road",
			"city": "Lyon",
			"stateProvince": "Lyon",
			"postalCode": "123456",
			"country": "FR"
		},
		"subjectName": {
			"title": "Mr.",
			"firstName": "Einstein ",
			"middleName": "James",
			"lastName": "Bela",
			"fullName": "Einstien James Bela"
		}
	},
	"recipientKyc": {
		"nationality": "FR",
		"dateOfBirth": "28-06-1986",
		"idDocument": [
			{
				"idType": "nationalidcard",
				"idNumber": "123456789",
				"issueDate": "2003-09-26",
				"expiryDate": "2033-09-26",
				"issuerCountry": "FR"
			}
		],
		"postalAddress": {
			"addressLine1": "49 ",
			"addressLine2": "park street",
			"addressLine3": "walton's road",
			"city": "Lyon",
			"stateProvince": "Lyon",
			"postalCode": "123456",
			"country": "FR"
		},
		"subjectName": {
			"firstName": "John",
			"lastName": "Smith",
			"fullName": "John Dave Smith"
		}
	},
	"internationalTransferInformation": {
		"quoteId": "QT037fQXs3LGWXea4",
		"receivingCountry": "NG",
		"remittancePurpose": "Gift",
		"sourceOfFunds": "Salary",
		"relationshipSender": "Brother"
	}
}
```

```javascript-screen-6
var myHeaders = new Headers();
myHeaders.append("X-USERNAME", "terrapayuser");
myHeaders.append("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b");
myHeaders.append("X-DATE", "2018-04-04 09:27:16");
myHeaders.append("X-ORIGINCOUNTRY", "US");
myHeaders.append("Content-Type", "text/plain");

var raw = "{\r\n  \"amount\": \"500\",\r\n  \"currency\": \"INR\",\r\n  \"type\": \"inttransfer\",\r\n  \"descriptionText\": \"Gift for my brother\",\r\n  \"requestDate\": \"2021-05-23 08:19:36\",\r\n  \"requestingOrganisationTransactionReference\": \"SrcTxnId002\",\r\n  \"debitParty\": [\r\n    {\r\n      \"key\": \"msisdn\",\r\n      \"value\": \"+971810456234\"\r\n    }\r\n  ],\r\n  \"creditParty\": [\r\n    {\r\n      \"key\": \"bankaccountno\",\r\n      \"value\": \"50100002965304\"\r\n    },\r\n    {\r\n      \"key\": \"organisationid\",\r\n      \"value\": \"HDFC Bank\"\r\n    },\r\n    {\r\n      \"key\": \"sortcode\",\r\n      \"value\": \"HDFC0001626\"\r\n    }\r\n  ],\r\n  \"senderKyc\": {\r\n    \"nationality\": \"AE\",\r\n    \"dateOfBirth\": \"1967-05-28\",\r\n    \"gender\": \"M\",\r\n    \"idDocument\": [\r\n      {\r\n        \"idType\": \"VOTER_CARD\",\r\n        \"idNumber\": \"13321115521\",\r\n        \"issueDate\": \"1967-05-28\",\r\n        \"expiryDate\": \"2067-05-28\",\r\n        \"issuerCountry\": \"AE\"\r\n      }\r\n    ],\r\n    \"postalAddress\": {\r\n      \"addressLine1\": \"49 , park street\",\r\n      \"addressLine2\": \"12\",\r\n      \"addressLine3\": \"12\",\r\n      \"city\": \"12\",\r\n      \"stateProvince\": \"12\",\r\n      \"postalCode\": \"50000\",\r\n      \"country\": \"US\"\r\n    },\r\n    \"subjectName\": {\r\n      \"firstName\": \"Test\",\r\n      \"middleName\": \"\",\r\n      \"lastName\": \"Sender2\",\r\n      \"fullName\": \"Test Sender2\"\r\n    }\r\n  },\r\n    \"recipientKyc\": {\r\n    \"subjectName\": {\r\n      \"firstName\": \"Deepa\",\r\n      \"lastName\": \"Jain\",\r\n      \"fullName\": \"Deepa Jain\"\r\n    }\r\n  },\r\n  \"internationalTransferInformation\": {\r\n    \"quoteId\": \"QR037C1NA6ZXBSQ88B\",\r\n    \"receivingCountry\": \"IN\",\r\n    \"remittancePurpose\": \"Family Maintainance\",\r\n    \"sourceOfFunds\": \"Salary\",\r\n    \"relationshipSender\": \"Brother\"\r\n  }\r\n}";

var requestOptions = {
  method: 'POST',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("https://uat-connect.terrapay.com:21211/eig/gsma/transactions", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```
```python-screen-6
import requests

url = "https://uat-connect.terrapay.com:21211/eig/gsma/transactions"

payload = "{\r\n  \"amount\": \"500\",\r\n  \"currency\": \"INR\",\r\n  \"type\": \"inttransfer\",\r\n  \"descriptionText\": \"Gift for my brother\",\r\n  \"requestDate\": \"2021-05-23 08:19:36\",\r\n  \"requestingOrganisationTransactionReference\": \"SrcTxnId002\",\r\n  \"debitParty\": [\r\n    {\r\n      \"key\": \"msisdn\",\r\n      \"value\": \"+971810456234\"\r\n    }\r\n  ],\r\n  \"creditParty\": [\r\n    {\r\n      \"key\": \"bankaccountno\",\r\n      \"value\": \"50100002965304\"\r\n    },\r\n    {\r\n      \"key\": \"organisationid\",\r\n      \"value\": \"HDFC Bank\"\r\n    },\r\n    {\r\n      \"key\": \"sortcode\",\r\n      \"value\": \"HDFC0001626\"\r\n    }\r\n  ],\r\n  \"senderKyc\": {\r\n    \"nationality\": \"AE\",\r\n    \"dateOfBirth\": \"1967-05-28\",\r\n    \"gender\": \"M\",\r\n    \"idDocument\": [\r\n      {\r\n        \"idType\": \"VOTER_CARD\",\r\n        \"idNumber\": \"13321115521\",\r\n        \"issueDate\": \"1967-05-28\",\r\n        \"expiryDate\": \"2067-05-28\",\r\n        \"issuerCountry\": \"AE\"\r\n      }\r\n    ],\r\n    \"postalAddress\": {\r\n      \"addressLine1\": \"49 , park street\",\r\n      \"addressLine2\": \"12\",\r\n      \"addressLine3\": \"12\",\r\n      \"city\": \"12\",\r\n      \"stateProvince\": \"12\",\r\n      \"postalCode\": \"50000\",\r\n      \"country\": \"US\"\r\n    },\r\n    \"subjectName\": {\r\n      \"firstName\": \"Test\",\r\n      \"middleName\": \"\",\r\n      \"lastName\": \"Sender2\",\r\n      \"fullName\": \"Test Sender2\"\r\n    }\r\n  },\r\n    \"recipientKyc\": {\r\n    \"subjectName\": {\r\n      \"firstName\": \"Deepa\",\r\n      \"lastName\": \"Jain\",\r\n      \"fullName\": \"Deepa Jain\"\r\n    }\r\n  },\r\n  \"internationalTransferInformation\": {\r\n    \"quoteId\": \"QR037C1NA6ZXBSQ88B\",\r\n    \"receivingCountry\": \"IN\",\r\n    \"remittancePurpose\": \"Family Maintainance\",\r\n    \"sourceOfFunds\": \"Salary\",\r\n    \"relationshipSender\": \"Brother\"\r\n  }\r\n}"
headers = {
  'X-USERNAME': 'terrapayuser',
  'X-PASSWORD': '101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b',
  'X-DATE': '2018-04-04 09:27:16',
  'X-ORIGINCOUNTRY': 'US',
  'Content-Type': 'text/plain'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)

```
```java-screen-6
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
MediaType mediaType = MediaType.parse("text/plain");
RequestBody body = RequestBody.create(mediaType, "{\r\n  \"amount\": \"500\",\r\n  \"currency\": \"INR\",\r\n  \"type\": \"inttransfer\",\r\n  \"descriptionText\": \"Gift for my brother\",\r\n  \"requestDate\": \"2021-05-23 08:19:36\",\r\n  \"requestingOrganisationTransactionReference\": \"SrcTxnId002\",\r\n  \"debitParty\": [\r\n    {\r\n      \"key\": \"msisdn\",\r\n      \"value\": \"+971810456234\"\r\n    }\r\n  ],\r\n  \"creditParty\": [\r\n    {\r\n      \"key\": \"bankaccountno\",\r\n      \"value\": \"50100002965304\"\r\n    },\r\n    {\r\n      \"key\": \"organisationid\",\r\n      \"value\": \"HDFC Bank\"\r\n    },\r\n    {\r\n      \"key\": \"sortcode\",\r\n      \"value\": \"HDFC0001626\"\r\n    }\r\n  ],\r\n  \"senderKyc\": {\r\n    \"nationality\": \"AE\",\r\n    \"dateOfBirth\": \"1967-05-28\",\r\n    \"gender\": \"M\",\r\n    \"idDocument\": [\r\n      {\r\n        \"idType\": \"VOTER_CARD\",\r\n        \"idNumber\": \"13321115521\",\r\n        \"issueDate\": \"1967-05-28\",\r\n        \"expiryDate\": \"2067-05-28\",\r\n        \"issuerCountry\": \"AE\"\r\n      }\r\n    ],\r\n    \"postalAddress\": {\r\n      \"addressLine1\": \"49 , park street\",\r\n      \"addressLine2\": \"12\",\r\n      \"addressLine3\": \"12\",\r\n      \"city\": \"12\",\r\n      \"stateProvince\": \"12\",\r\n      \"postalCode\": \"50000\",\r\n      \"country\": \"US\"\r\n    },\r\n    \"subjectName\": {\r\n      \"firstName\": \"Test\",\r\n      \"middleName\": \"\",\r\n      \"lastName\": \"Sender2\",\r\n      \"fullName\": \"Test Sender2\"\r\n    }\r\n  },\r\n    \"recipientKyc\": {\r\n    \"subjectName\": {\r\n      \"firstName\": \"Deepa\",\r\n      \"lastName\": \"Jain\",\r\n      \"fullName\": \"Deepa Jain\"\r\n    }\r\n  },\r\n  \"internationalTransferInformation\": {\r\n    \"quoteId\": \"QR037C1NA6ZXBSQ88B\",\r\n    \"receivingCountry\": \"IN\",\r\n    \"remittancePurpose\": \"Family Maintainance\",\r\n    \"sourceOfFunds\": \"Salary\",\r\n    \"relationshipSender\": \"Brother\"\r\n  }\r\n}");
Request request = new Request.Builder()
  .url("https://uat-connect.terrapay.com:21211/eig/gsma/transactions")
  .method("POST", body)
  .addHeader("X-USERNAME", "terrapayuser")
  .addHeader("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b")
  .addHeader("X-DATE", "2018-04-04 09:27:16")
  .addHeader("X-ORIGINCOUNTRY", "US")
  .addHeader("Content-Type", "text/plain")
  .build();
Response response = client.newCall(request).execute();
```
```ruby-screen-6
require "uri"
require "net/http"

url = URI("https://uat-connect.terrapay.com:21211/eig/gsma/transactions")

https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true

request = Net::HTTP::Post.new(url)
request["X-USERNAME"] = "terrapayuser"
request["X-PASSWORD"] = "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b"
request["X-DATE"] = "2018-04-04 09:27:16"
request["X-ORIGINCOUNTRY"] = "US"
request["Content-Type"] = "text/plain"
request.body = "{\r\n  \"amount\": \"500\",\r\n  \"currency\": \"INR\",\r\n  \"type\": \"inttransfer\",\r\n  \"descriptionText\": \"Gift for my brother\",\r\n  \"requestDate\": \"2021-05-23 08:19:36\",\r\n  \"requestingOrganisationTransactionReference\": \"SrcTxnId002\",\r\n  \"debitParty\": [\r\n    {\r\n      \"key\": \"msisdn\",\r\n      \"value\": \"+971810456234\"\r\n    }\r\n  ],\r\n  \"creditParty\": [\r\n    {\r\n      \"key\": \"bankaccountno\",\r\n      \"value\": \"50100002965304\"\r\n    },\r\n    {\r\n      \"key\": \"organisationid\",\r\n      \"value\": \"HDFC Bank\"\r\n    },\r\n    {\r\n      \"key\": \"sortcode\",\r\n      \"value\": \"HDFC0001626\"\r\n    }\r\n  ],\r\n  \"senderKyc\": {\r\n    \"nationality\": \"AE\",\r\n    \"dateOfBirth\": \"1967-05-28\",\r\n    \"gender\": \"M\",\r\n    \"idDocument\": [\r\n      {\r\n        \"idType\": \"VOTER_CARD\",\r\n        \"idNumber\": \"13321115521\",\r\n        \"issueDate\": \"1967-05-28\",\r\n        \"expiryDate\": \"2067-05-28\",\r\n        \"issuerCountry\": \"AE\"\r\n      }\r\n    ],\r\n    \"postalAddress\": {\r\n      \"addressLine1\": \"49 , park street\",\r\n      \"addressLine2\": \"12\",\r\n      \"addressLine3\": \"12\",\r\n      \"city\": \"12\",\r\n      \"stateProvince\": \"12\",\r\n      \"postalCode\": \"50000\",\r\n      \"country\": \"US\"\r\n    },\r\n    \"subjectName\": {\r\n      \"firstName\": \"Test\",\r\n      \"middleName\": \"\",\r\n      \"lastName\": \"Sender2\",\r\n      \"fullName\": \"Test Sender2\"\r\n    }\r\n  },\r\n    \"recipientKyc\": {\r\n    \"subjectName\": {\r\n      \"firstName\": \"Deepa\",\r\n      \"lastName\": \"Jain\",\r\n      \"fullName\": \"Deepa Jain\"\r\n    }\r\n  },\r\n  \"internationalTransferInformation\": {\r\n    \"quoteId\": \"QR037C1NA6ZXBSQ88B\",\r\n    \"receivingCountry\": \"IN\",\r\n    \"remittancePurpose\": \"Family Maintainance\",\r\n    \"sourceOfFunds\": \"Salary\",\r\n    \"relationshipSender\": \"Brother\"\r\n  }\r\n}"

response = https.request(request)
puts response.read_body

```


> Success Response: 

```json
{
	"amount": "100000.01",
	"currency": "NGN",
	"type": "inttransfer",
	"requestDate": "2017-03-20T06:19:36.969Z",
	"requestingOrganisationTransactionReference": "partnerRefId1234",
	"debitParty": [
		{
			"key": "msisdn",
			"value": "+33472034605"
		} 
	],
	"creditParty": [
		{
			"key": "msisdn",
			"value": "+23410706056"
		}
	],
	"transactionStatus": "3000:Remit Success",
	"transactionReference": "TPKM000000056269"  
}

```

> Failure Response : 

```json
{
	"serverCorrelationId":"TPKM000000056269", 
	"clientCorrelationId":"partnerRefId1234",
	"error": {
		"errorCategory":"authorisation", 
		"errorCode":"1003", 
		"errorDescription":"Authentication failed. Username or Password is incorrect.", 
		"errorDateTime":"2017-05-02 11:00:00"
	}
}

```

```json
{
	"serverCorrelationId":"TPKM000000056269", 
	"clientCorrelationId":"partnerRefId1234",
	"error": {
		"errorCategory":"businessRule", 
		"errorCode":"3032", 
		"errorDescription":"Remit Failed.", 
		"errorDateTime":"2017-05-02 11:00:00"
	}
}
```
### URL
https://uat-connect.terrapay.com:21211/eig/gsma/transactions

### HTTP Request
`POST /eig/gsma/transactions HTTP/1.1`

### Request Parameters

Parameter|Description|Data Type|Requirement|Field Length
--------- | ----------- |----------|---------|------------
requestDate| The creation date and time of the transaction as supplied by the client in YYYY-MM-DD HH:mm:ss| String|Mandatory|19
amount| Destination amount payable to the beneficiary with precision of 2 decimal places. |String|Mandatory|	10,2
currency | Destination amount currency in ISO 4217 format. Eg. NGN	|String|Mandatory|3
type | The harmonized Transaction Type. Fixed default value "inttransfer"	|String|	Mandatory	|11
descriptionText | Free format text description of the transaction provided by the client. This can be provided as a reference for the receiver on the SMS and on the account statement.	|String	|Optional|	0-20
requestingOrganisationTransactionReference | Unique Transaction reference generated by the sending partner.	|String|Mandatory|4-50
provider | Provider value should be same as sent in the validation request. If a different value is sent then the transaction will be rejected.<aside class="success">**NOTE**:Mandatory for transactions to Bangladesh (bank & wallet), China (bank & wallet), Nepal (wallet), Pakistan (wallet), Philippines (wallet), South Sudan (wallet), Indonesia (wallet).Optional for other countries.</aside> |Numeric	|Optional|5-12
debitParty:	|
key | msisdn |String|	Mandatory|	6
value | Sender Mobile Number with country code. Eg. +91xxxxxxxxxx	|String	|Mandatory	|10-18
creditParty:|
key | msisdn |String|Conditional|6
value | Beneficiary Mobile Number with country code. Eg.+91xxxxxxxxxx.|String|Optional - For Bank Accounts and Mandatory - For Mobile Wallet|10-18
key | bankaccountno |String|Conditional|13
value |Beneficiary Bank Account or IBAN Number as applicable in the destination country for receiving funds. Eg. 2365417895.This key/value pair is optional if the transfer is to a mobile wallet. |String|Mandatory - For Bank Accounts and Optional - For Mobile Wallet|5-50
key | sortcode |String|Conditional|8
value |	Bank Code as required in the destination Country. It can be one of IFSC Code, Routing Code,Swift BIC. This code is specific to bank integration in each country |String|Mandatory - For bank accounts and Optional - For mobile wallets|4-25
key | organisationid |String|Conditional|14
value | Full name of the beneficiary bank	|String|Mandatory - For bank accounts and Optional - For mobile wallets|4-60
key | banksubcode |String|Conditional|1-10
value | This is a code that indicates the branch code of the specific bank to which the transaction is to be sent.<aside class="success">**NOTE**: Mandatory for bank transactions to Brazil & Uruguay.Optional for other countries. If the transaction is to Bangladesh then partner can send rounting number in banksubcode and they do not have to send the provider code.</aside> |String|Mandatory - For bank accounts and Optional - For mobile wallets|1-10
senderKyc:|
nationality | Nationality of the customer in ISO Alpha-2 format. Eg. US	 |String|Mandatory|	2
dateOfBirth | Customer's Date of Birth in YYYY-MM-DD format	 |String|Mandatory|10
gender | Customer's Gender. Enumeration = (M)ale, (F)emale, (U)nspecified	 |String|Optional|1
senderKyc:idDocument:|
idType | Customer's Id document type: nationalidcard , drivinglicense ,passport |String	|Mandatory|	1-20
idNumber | 	Customer's Id number. For any other type, it should be Passport Number,Document number. Eg. M123456,123434567 |String	|Mandatory|	1-30
issueDate | Customer's Id document issue date in YYYY-MM-DD format. |String	|Optional|	10
expiryDate | Customer's Id document expiry date in YYYY-MM-DD format. |String	|Mandatory|	10
issuerCountry | Country where the identification type was issued in ISO Alpha-2 format.	|String	|Optional|	2
senderKyc:postalAddress:|
addressLine1 | First line of the address	|String|Mandatory|4-20
addressLine2	 | Second line of the address	 |String|	Optional|	4-20
addressLine3 | Third line of the address	|String|	Optional|	4-20
city | City/Town of sender's address |String|	Mandatory|	4-20
state | State of sender's address |String|	Optional|	4-20
postalCode | Postal Code of sender's address |String|	Optional|	6-8	
country | Country in ISO Alpha-2 format |String|	Mandatory|	2
senderKyc:subjectName:|
title	| Title of the Sender |String|Optional|0-6
firstName	| First name of the Sender |String|Mandatory	|1-20
middleName | Middle name of the Sender |String|Optional|0-50
lastName | Last name of the Sender |String|Mandatory	|1-20
fullName |Full name of the Sender|String|Mandatory	|1-50
recipientKyc:|
nationality|	Nationality of the customer in ISO Alpha-2 format. Eg. US	|String	|Conditional|	2
dateOfBirth	|Customer's Date of Birth in YYYY-MM-DD format|	String|	Conditional|	10
recipientKyc:idDocument:|
idType|Customer's Id document type:nationalidcard,drivinglicense,passport|	String|	Conditional|	1-20
idNumber|Customer's Id number.For any other type, it should be Passport Number,Document number. Eg. M123456,123434567	|String|	Conditional|	1-30
issueDate|	Customer's Id document issue date in YYYY-MM-DD format.|String|	Optional|	10
expiryDate|	Customer's Id document expiry date in YYYY-MM-DD format.|String	|Conditional|	10
issuerCountry	|Country where the identification type was issued in ISO Alpha-2 format.|	String|Optional|2
recipientKyc:postalAddress:|
addressLine1	|First line of the address|	String|	Conditional	|4-20
addressLine2|	Second line of the address|	String|	Optional|	4-20
addressLine3|	Third line of the address	|String	|Optional|	4-20
city|	City/Town of sender's address|	String|	Conditional|	4-20
stateProvince	|State of sender's address|	String|	Optional|	4-20
postalCode|	Postal Code of sender's address|	String|	Optional|	6-8
country	|Country in ISO Alpha-2 format|	String|	Conditional|2
recipientKyc:subjectName:|
firstName	| First name of the recipient |String|Mandatory	|1-20
lastName | Last name of the recipient |String|Mandatory	|1-20
fullName | Full name of the recipient |String|Mandatory	|1-50
internationalTransferInformation:	|
quoteId	| The specific quoteId to be used for the transaction. |String|Mandatory|16-20
receivingCountry | Destination Country of international remittance in ISO Alpha 2 format. Eg. NG |String|Mandatory|2
remittancePurpose | Reason for the transfer.|String|Mandatory|4-30
sourceOfFunds	| Source of funds. |String|Mandatory|4-17
relationshipSender | The relation between the sender and the beneficiary.|String|Mandatory|3-11


### Response Parameters

 Parameter | Description |Data Type|
 --------- | ----------- |----------
 requestDate | The creation date and time of the transaction as supplied by the client.	|String
 amount|	Principle  Transaction Amount.|String
 currency	| Currency of the principal transaction amount.|String
 type	| The harmonised Transaction Type|String
 requestingOrganisationTransactionReference	| Unique Transaction reference submitted by sending partner as part of request buffer.|String
 transactionStatus	| Indicates the status of the transaction|String
 transactionReference	| Unique reference for the transaction. This is returned in the response by Terrapay's system|String
 debitParty:	|
 key	| msisdn|String	
 value	| Sender Mobile Number as sent by the partner in the request API|String
 creditParty:	|
 key | msisdn|String
 value | Beneficiary Mobile Number as sent by the partner in the request API|String
 key | bankaccountno|String
 value | Beneficiary bank account details as sent by the partner in the request API	|String

## View A Transaction
The View Transactions API is used for looking up the status of a transaction already sent to the TerraPay system. 

**URI format is:** /transactions/{transactionReference}
### View Transaction Status to a Mobile Wallet <a class="tryitbutton" href='https://developers.terrapay.com/try-it/view-transaction-mobile' target="_blank">Try it </a>
> View Transaction Status to a Mobile Wallet

```shell-screen-7

curl --location --request GET 'https://uat-connect.terrapay.com:21211/eig/gsma/transactions/TPPU000000334449' \
--header 'Content-Type: application/json'\
--header 'X-USERNAME:terrapayuser' \
--header 'X-PASSWORD: 101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b' \
--header 'X-DATE: 2020-01-02 10:51:16' \
--header 'X-ORIGINCOUNTRY: US' \


```

```javascript-screen-7
var myHeaders = new Headers();
myHeaders.append("X-USERNAME", "terrapayuser");
myHeaders.append("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b");
myHeaders.append("X-DATE", "2018-04-04 09:27:16");
myHeaders.append("X-ORIGINCOUNTRY", "US");

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  redirect: 'follow'
};

fetch("https://uat-connect.terrapay.com:21211/eig/gsma/transactions/SrcTxnId001", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```python-screen-7
import requests

url = "https://uat-connect.terrapay.com:21211/eig/gsma/transactions/SrcTxnId001"

payload={}
headers = {
  'X-USERNAME': 'terrapayuser',
  'X-PASSWORD': '101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b',
  'X-DATE': '2018-04-04 09:27:16',
  'X-ORIGINCOUNTRY': 'US'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)

```

```java-screen-7
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
Request request = new Request.Builder()
  .url("https://uat-connect.terrapay.com:21211/eig/gsma/transactions/SrcTxnId001")
  .method("GET", null)
  .addHeader("X-USERNAME", "terrapayuser")
  .addHeader("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b")
  .addHeader("X-DATE", "2018-04-04 09:27:16")
  .addHeader("X-ORIGINCOUNTRY", "US")
  .build();
Response response = client.newCall(request).execute();
```

```ruby-screen-7
require "uri"
require "net/http"

url = URI("https://uat-connect.terrapay.com:21211/eig/gsma/transactions/SrcTxnId001")

https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true

request = Net::HTTP::Get.new(url)
request["X-USERNAME"] = "terrapayuser"
request["X-PASSWORD"] = "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b"
request["X-DATE"] = "2018-04-04 09:27:16"
request["X-ORIGINCOUNTRY"] = "US"

response = https.request(request)
puts response.read_body

```

> Success Response  

```json
{
	"amount": "100000.01",
	"currency": "NGN",
	"type": "inttransfer",
	"requestDate": "2017-03-20T06:19:36.969Z",
	"requestingOrganisationTransactionReference": "partnerRefId1234",
	"debitParty": [
		{
   			"key": "msisdn",
   			"value": "+33472034605"
		}
	],
	"creditParty": [
		{
			"key": "msisdn",
			"value": "+23410706056"
		}
	],
	"transactionStatus": "3000:Remit Success",
	"transactionReference": "TPKM000000056269"  
}


```

> Failure Response : 

```json
{
	"serverCorrelationId":"", 
	"clientCorrelationId":"partnerRefId1234",
	"error": {
		"errorCategory":"authorisation", 
		"errorCode":"1003", 
		"errorDescription":"Authentication failed. Username or Password is incorrect.", 
		"errorDateTime":"2017-05-02 11:00:00"
	}
}

```

```json
{
	"serverCorrelationId":"TPKM000000056269", 
	"clientCorrelationId":"partnerRefId1234",
	"error": {
		"errorCategory":"businessRule", 
		"errorCode":"3032", 
		"errorDescription":"Remit Failed.", 
		"errorDateTime":"2017-05-02 11:00:00"
	}
}

```
### URL
https://uat-connect.terrapay.com:21211/eig/gsma/transactions/{transactionReference}

### HTTP Request
`GET /eig/gsma/transactions/TPKM000000056269 HTTP/1.1`

### View Transaction Status to a Bank Account <a class="tryitbutton" href='https://developers.terrapay.com/try-it/view-transaction-bank' target="_blank">Try it </a>

> View Transaction Status to a Bank Account

 ```shell-screen-8

curl --location --request GET 'https://uat-connect.terrapay.com:21211/eig/gsma/transactions/TPKM000000056269 HTTP/1.1'\
--header  'Content-Type: application/json'\
--header  'X-USERNAME: terrapayuser '\
--header  'X-PASSWORD: 101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b'\
--header  'X-DATE: "2017-05-03 11:00:00'\
--header  'X-ORIGINCOUNTRY:US'\
```

```javascript-screen-8
var myHeaders = new Headers();
myHeaders.append("X-USERNAME", "terrapayuser");
myHeaders.append("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b");
myHeaders.append("X-DATE", "2018-04-04 09:27:16");
myHeaders.append("X-ORIGINCOUNTRY", "US");

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  redirect: 'follow'
};

fetch("https://uat-connect.terrapay.com:21211/eig/gsma/transactions/SrcTxnId001", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```python-screen-8
import requests

url = "https://uat-connect.terrapay.com:21211/eig/gsma/transactions/SrcTxnId001"

payload={}
headers = {
  'X-USERNAME': 'terrapayuser',
  'X-PASSWORD': '101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b',
  'X-DATE': '2018-04-04 09:27:16',
  'X-ORIGINCOUNTRY': 'US'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)

```
```java-screen-8
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
Request request = new Request.Builder()
  .url("https://uat-connect.terrapay.com:21211/eig/gsma/transactions/SrcTxnId001")
  .method("GET", null)
  .addHeader("X-USERNAME", "terrapayuser")
  .addHeader("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b")
  .addHeader("X-DATE", "2018-04-04 09:27:16")
  .addHeader("X-ORIGINCOUNTRY", "US")
  .build();
Response response = client.newCall(request).execute();
```
```ruby-screen-8
require "uri"
require "net/http"

url = URI("https://uat-connect.terrapay.com:21211/eig/gsma/transactions/SrcTxnId001")

https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true

request = Net::HTTP::Get.new(url)
request["X-USERNAME"] = "terrapayuser"
request["X-PASSWORD"] = "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b"
request["X-DATE"] = "2018-04-04 09:27:16"
request["X-ORIGINCOUNTRY"] = "US"

response = https.request(request)
puts response.read_body

```
> Success Response
 
 ```json
  {
	"amount": "100000.01",
	"currency": "NGN",
	"type": "inttransfer",
	"requestDate": "2017-03-20T06:19:36.969Z",
	"requestingOrganisationTransactionReference": "partnerRefId1234",
	"debitParty": [
		{
			"key": "msisdn",
			"value": "+33472034605"
		} 
	],
	"creditParty": [
		{
			"key": "msisdn",
			"value": "+23410706056"
		}
	],
	"transactionStatus": "3000:Remit Success",
	"transactionReference": "TPKM000000056269"  
}
```
> Failure Response:

```json
{
	"serverCorrelationId":"", 
	"clientCorrelationId":"partnerRefId1234",
	"error": {
		"errorCategory":"authorisation", 
		"errorCode":"1003", 
		"errorDescription":"Authentication failed. Username or Password is incorrect.", 
		"errorDateTime":"2017-05-02 11:00:00"
	}
}
{
	"serverCorrelationId":"TPKM000000056269", 
	"clientCorrelationId":"partnerRefId1234",
	"error": {
		"errorCategory":"businessRule", 
		"errorCode":"3032", 
		"errorDescription":"Remit Failed.", 
		"errorDateTime":"2017-05-02 11:00:00"
	}
}

	
```
### URL
https://uat-connect.terrapay.com:21211/eig/gsma/transactions/{transactionReference}

### HTTP Request
`GET /eig/gsma/transactions/TPKM000000056269 HTTP/1.1`
### Request Parameters

Parameter | Description |Data Type	|Requirement
--------- | ----------- |-----------|--------------
transactionReference | Unique reference for the transaction which was returned in the response of the createTransaction API or the unique reference generated by the partner's system and sent in the createTransaction API request.|String|Mandatory

### Response Parameters

 Parameter | Description |Data Type
 --------- | ----------- |-----------
 requestDate | The creation date and time of the transaction as supplied by the client.	|String
 amount	| Principle Transaction Amount.|String
 currency	| Currency of the principal transaction amount.|String
 type	| The harmonised Transaction Type|String
 requestingOrganisationTransactionReference	| Unique Transaction reference generated by the sending partner.|String
 transactionStatus	| Indicates the status of the transaction|String
 transactionReference	| Unique reference for the transaction. This is returned in the response by Terrapay's system|String
 debitParty:	|
 key	| The name of the debitparty account identifier	|String	
 value	| Keys include MSISDN and Wallet Identifier	|String
 creditParty:	|
 key | The name of the creditparty account identifier	|String
 value | Keys include MSISDN and Wallet Identifier	|String



## Ledger Balance 


The ledger balance API is used for get the current balance in the partner's ledger. The balance can be retrieved for a particular currency ledger or all currencies ledger. The ledger balance is retrieved only if the ledger is active. 

**URI format is:** accounts/{currency}/balance


> Get Balance of all ledgers 

```shell-screen-9
curl --location --request GET 'https://uat-connect.terrapay.com:21211/eig/gsma/accounts/all/balance'\
--header 'X-USERNAME:terrapayuser '\
--header 'X-PASSWORD: 101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b'\
--header 'X-DATE: 2017-05-03 11:00:00'\
--header 'X-ORIGINCOUNTRY:US'\
--header 'Content-Type: application/json '
```
```javascript-screen-9
var myHeaders = new Headers();
myHeaders.append("X-USERNAME", "terrapayuser");
myHeaders.append("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b");
myHeaders.append("X-DATE", "2018-04-04 09:27:16");
myHeaders.append("X-ORIGINCOUNTRY", "US");

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  redirect: 'follow'
};

fetch("https://uat-connect.terrapay.com:21211/eig/gsma/accounts/all/balance", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```
```python-screen-9
import requests

url = "https://uat-connect.terrapay.com:21211/eig/gsma/accounts/all/balance"

payload={}
headers = {
  'X-USERNAME': 'terrapayuser',
  'X-PASSWORD': '101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b',
  'X-DATE': '2018-04-04 09:27:16',
  'X-ORIGINCOUNTRY': 'US'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)

```
```java-screen-9
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
Request request = new Request.Builder()
  .url("https://uat-connect.terrapay.com:21211/eig/gsma/accounts/all/balance")
  .method("GET", null)
  .addHeader("X-USERNAME", "terrapayuser")
  .addHeader("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b")
  .addHeader("X-DATE", "2018-04-04 09:27:16")
  .addHeader("X-ORIGINCOUNTRY", "US")
  .build();
Response response = client.newCall(request).execute();
```
```ruby-screen-9
require "uri"
require "net/http"

url = URI("https://uat-connect.terrapay.com:21211/eig/gsma/accounts/all/balance")

https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true

request = Net::HTTP::Get.new(url)
request["X-USERNAME"] = "terrapayuser"
request["X-PASSWORD"] = "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b"
request["X-DATE"] = "2018-04-04 09:27:16"
request["X-ORIGINCOUNTRY"] = "US"

response = https.request(request)
puts response.read_body

```
> Success Response: 


```json
[
	{
		"currency": "USD",
		"currentBalance": "1000.000000",
		"status": "available"
	},
	{
		"currency": "NGN",
		"currentBalance": "3000000.000000",
		"status": "available"
	},
	{
		"currency": "TZS",
		"currentBalance": "1000000.000000",
		"status": "available"
	}
]

```

> Get Balance for a single currency ledger

```shell-screen-ten
curl --location --request GET 'https://uat-connect.terrapay.com:21211/eig/gsma/accounts/USD/balance'\
--header 'X-USERNAME: terrapayuser'\
--header 'X-PASSWORD: 101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b'\
--header 'X-DATE: 2017-05-03 11:00:00'\
--header 'X-ORIGINCOUNTRY:US'\
--header 'Content-Type: application/json'
```
```javascript-screen-ten
var myHeaders = new Headers();
myHeaders.append("X-USERNAME", "terrapayuser");
myHeaders.append("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b");
myHeaders.append("X-DATE", "2018-04-04 09:27:16");
myHeaders.append("X-ORIGINCOUNTRY", "US");

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  redirect: 'follow'
};

fetch("https://uat-connect.terrapay.com:21211/eig/gsma/accounts/USD/balance", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```
```python-screen-ten
import requests

url = "https://uat-connect.terrapay.com:21211/eig/gsma/accounts/USD/balance"

payload={}
headers = {
  'X-USERNAME': 'terrapayuser',
  'X-PASSWORD': '101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b',
  'X-DATE': '2018-04-04 09:27:16',
  'X-ORIGINCOUNTRY': 'US'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```
```java-screen-ten
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
Request request = new Request.Builder()
  .url("https://uat-connect.terrapay.com:21211/eig/gsma/accounts/USD/balance")
  .method("GET", null)
  .addHeader("X-USERNAME", "terrapayuser")
  .addHeader("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b")
  .addHeader("X-DATE", "2018-04-04 09:27:16")
  .addHeader("X-ORIGINCOUNTRY", "US")
  .build();
Response response = client.newCall(request).execute();
```
```ruby-screen-ten
require "uri"
require "net/http"

url = URI("https://uat-connect.terrapay.com:21211/eig/gsma/accounts/USD/balance")

https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true

request = Net::HTTP::Get.new(url)
request["X-USERNAME"] = "terrapayuser"
request["X-PASSWORD"] = "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b"
request["X-DATE"] = "2018-04-04 09:27:16"
request["X-ORIGINCOUNTRY"] = "US"

response = https.request(request)
puts response.read_body
```
> Success Response: 


```json
[
	{
		"currency": "USD",
		"currentBalance": "1000.000000",
		"status": "available"
	}
]
	
```
### Get Balance of all ledgers <a class="tryitbutton" href='https://developers.terrapay.com/try-it/ledger' target="_blank">Try it </a>
### URL
https://uat-connect.terrapay.com:21211/eig/gsma/accounts/all/balance
### HTTP Request
`GET /eig/gsma/accounts/all/balance HTTP/1.1`

### Get Balance for a single currency ledger <a class="tryitbutton" href='https://developers.terrapay.com/try-it/ledger' target="_blank">Try it </a>

### URL
https://uat-connect.terrapay.com:21211/eig/gsma/accounts/USD/balance

### HTTP Request
`GET /eig/gsma/accounts/USD/balance HTTP/1.1`

## Corridor Quotation 

### Corridor Quotation <a class="tryitbutton" href='https://developers.terrapay.com/try-it/corridor-quotation' target="_blank">Try it </a>
> Corridor Quotation 


```shell-screen-eleven
curl --location --request GET'https://uat-connect.terrapay.com:21211/eig/gsma/quotations/all '\
--header 'X-USERNAME: terrapayuser'\
--header 'X-PASSWORD: 101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b'\
--header 'X-DATE: 2017-05-03 11:00:00'\
--header 'X-ORIGINCOUNTRY:US'\
--header 'Content-Type: application/json'
```
```javascript-screen-eleven
var myHeaders = new Headers();
myHeaders.append("X-USERNAME", "terrapayuser");
myHeaders.append("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b");
myHeaders.append("X-DATE", "2018-04-04 09:27:16");
myHeaders.append("X-ORIGINCOUNTRY", "US");

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  redirect: 'follow'
};

fetch("https://uat-connect.terrapay.com:21211/eig/gsma/quotations/all", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```
```python-screen-eleven
import requests

url = "https://uat-connect.terrapay.com:21211/eig/gsma/quotations/all"

payload={}
headers = {
  'X-USERNAME': 'terrapayuser',
  'X-PASSWORD': '101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b',
  'X-DATE': '2018-04-04 09:27:16',
  'X-ORIGINCOUNTRY': 'US'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)

```
```java-screen-eleven
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
Request request = new Request.Builder()
  .url("https://uat-connect.terrapay.com:21211/eig/gsma/quotations/all")
  .method("GET", null)
  .addHeader("X-USERNAME", "terrapayuser")
  .addHeader("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b")
  .addHeader("X-DATE", "2018-04-04 09:27:16")
  .addHeader("X-ORIGINCOUNTRY", "US")
  .build();
Response response = client.newCall(request).execute();
```
```ruby-screen-eleven
require "uri"
require "net/http"

url = URI("https://uat-connect.terrapay.com:21211/eig/gsma/quotations/all")

https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true

request = Net::HTTP::Get.new(url)
request["X-USERNAME"] = "terrapayuser"
request["X-PASSWORD"] = "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b"
request["X-DATE"] = "2018-04-04 09:27:16"
request["X-ORIGINCOUNTRY"] = "US"

response = https.request(request)
puts response.read_body

```
> Success Response

```json
[
    {
		"requestDate": "2017-10-18 09:27:16",
		"requestCurrency": "USD",
		"quotes":[
			{
				"receivingServiceProvider": "GH",
				"receivingCurrency": "GHS",
				"fxRate": "4.966000"
			},
			{
				"receivingServiceProvider": "UG",
				"receivingCurrency": "UGX",
				"fxRate": "3728.000597"
			}
		],
        	"quotationStatus": "9000:Success"
    }
]
 
```


This API is used to get the foreign exchange rates for the prefunding currency corridors that are active for the partner


**URI format is:**  /quotations/{prefunding_currency}

### URL
 https://uat-connect.terrapay.com:21211/eig/gsma/quotations/USD
### HTTP Request
`GET /eig/gsma/quotations/all HTTP/1.1`


## Cancel Transaction

### Cancel Transaction <a class="tryitbutton" href='https://developers.terrapay.com/try-it/cancel-transaction' target="_blank">Try it </a>

> Cancel Transaction

```shell-screen-twelve
curl --location --request POST 'https://uat-connect.terrapay.com:21211/eig/gsma/remitCancel/'\
 --header 'X-USERNAME: terrapayuser'\
 --header 'X-PASSWORD: 101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b'\
 --header 'X-DATE: "2021-01-03 11:00:00'\
 --header 'X-ORIGINCOUNTRY:US'\
 --header 'Content-Type: application/json'\
 --data-raw
   {
        "reason": "cancelling",
        "txnId": "TPSE000000298941"
   }
 
```

```javascript-screen-twelve
var myHeaders = new Headers();
myHeaders.append("X-USERNAME", "terrapayuser");
myHeaders.append("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b");
myHeaders.append("X-DATE", "2018-04-04 09:27:16");
myHeaders.append("X-ORIGINCOUNTRY", "US");
myHeaders.append("Content-Type", "application/json");

var raw = JSON.stringify({
  "reason": "cancelling",
  "txnId": "SrcTxnId001"
});

var requestOptions = {
  method: 'POST',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("https://uat-connect.terrapay.com:21211/eig/gsma/remitCancel", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```
```python-screen-twelve
import requests
import json

url = "https://uat-connect.terrapay.com:21211/eig/gsma/remitCancel"

payload = json.dumps({
  "reason": "cancelling",
  "txnId": "SrcTxnId001"
})
headers = {
  'X-USERNAME': 'terrapayuser',
  'X-PASSWORD': '101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b',
  'X-DATE': '2018-04-04 09:27:16',
  'X-ORIGINCOUNTRY': 'US',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)

```
```java-screen-twelve
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, "{\r\n    \"reason\": \"cancelling\",\r\n    \"txnId\": \"SrcTxnId001\"\r\n}");
Request request = new Request.Builder()
  .url("https://uat-connect.terrapay.com:21211/eig/gsma/remitCancel")
  .method("POST", body)
  .addHeader("X-USERNAME", "terrapayuser")
  .addHeader("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b")
  .addHeader("X-DATE", "2018-04-04 09:27:16")
  .addHeader("X-ORIGINCOUNTRY", "US")
  .addHeader("Content-Type", "application/json")
  .build();
Response response = client.newCall(request).execute();
```
```ruby-screen-twelve
require "uri"
require "json"
require "net/http"

url = URI("https://uat-connect.terrapay.com:21211/eig/gsma/remitCancel")

https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true

request = Net::HTTP::Post.new(url)
request["X-USERNAME"] = "terrapayuser"
request["X-PASSWORD"] = "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b"
request["X-DATE"] = "2018-04-04 09:27:16"
request["X-ORIGINCOUNTRY"] = "US"
request["Content-Type"] = "application/json"
request.body = JSON.dump({
  "reason": "cancelling",
  "txnId": "SrcTxnId001"
})

response = https.request(request)
puts response.read_body

```

> Success Response

```json
{
  "responseMessage": "Cancel Success",
   "statusCode": "15000"
 }
```

This API is used to cancel an initiated transaction which is not yet credited. The cancellation will be done only if the transaction is pending on the TerraPay system and has not already been sent to the receiving partner for credit to the beneficiary account

### URL
https://uat-connect.terrapay.com:21211/eig/gsma/remitCancel/

### HTTP Request

`POST /eig/gsma/remitCancel HTTP/1.1`

### Cancel transaction request parameter list

Parameter name |Description |Data Type|Requirement
--------- | ------- | -----------|--------
txnId |Reference for the transaction which was returned by transaction response buffer by Terrapay's system or partner transaction id.|String|Mandatory

### Response code for cancel transactions
Response Code | Response Message
-----------------|--------------------
15000 | Cancel Success
15001 | Cannot Cancel. Credit already in process.
15002 | Cannot Cancel. Transaction in Success state.
15003 | Cannot Cancel. Transaction in Fail state.
15004 | Cannot Cancel. Transaction not found.
15005 | Transaction already in canceled state.

## Reverse Transaction

### Reverse Transaction <a class="tryitbutton" href='https://developers.terrapay.com/try-it/reverse-transaction' target="_blank">Try it </a>

> Reverse Transaction


```shell-screen-thirteen
curl --location --request POST 'https://uat-connect.terrapay.com:21211/eig/gsma/reversalInitiate/'\
--header 'X-USERNAME: terrapayuser'\
--header 'X-PASSWORD: 101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b'\
--header 'X-DATE: 2021-01-03 11:00:00'\
--header 'X-ORIGINCOUNTRY:US'\
--header 'Content-Type: application/json'\
--data-raw

{
  "reversalReason": "reversalreason",
  "txnId": "TPKM000000056269"
}

```
```javascript-screen-thirteen
var myHeaders = new Headers();
myHeaders.append("X-USERNAME", "terrapayuser");
myHeaders.append("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b");
myHeaders.append("X-DATE", "2018-04-04 09:27:16");
myHeaders.append("X-ORIGINCOUNTRY", "US");
myHeaders.append("Content-Type", "application/json");

var raw = JSON.stringify({
  "reversalReason": "reversalreason",
  "txnId": "TPKM000000056269"
});

var requestOptions = {
  method: 'POST',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("https://uat-connect.terrapay.com:21211/eig/gsma/reversalInitiate", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```
```python-screen-thirteen
import requests
import json

url = "https://uat-connect.terrapay.com:21211/eig/gsma/reversalInitiate"

payload = json.dumps({
  "reversalReason": "reversalreason",
  "txnId": "TPKM000000056269"
})
headers = {
  'X-USERNAME': 'terrapayuser',
  'X-PASSWORD': '101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b',
  'X-DATE': '2018-04-04 09:27:16',
  'X-ORIGINCOUNTRY': 'US',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)

```
```java-screen-thirteen
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, "{\r\n    \"reversalReason\": \"reversalreason\",\r\n    \"txnId\": \"TPKM000000056269\"\r\n}");
Request request = new Request.Builder()
  .url("https://uat-connect.terrapay.com:21211/eig/gsma/reversalInitiate")
  .method("POST", body)
  .addHeader("X-USERNAME", "terrapayuser")
  .addHeader("X-PASSWORD", "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b")
  .addHeader("X-DATE", "2018-04-04 09:27:16")
  .addHeader("X-ORIGINCOUNTRY", "US")
  .addHeader("Content-Type", "application/json")
  .build();
Response response = client.newCall(request).execute();
```
```ruby-screen-thirteen
require "uri"
require "json"
require "net/http"

url = URI("https://uat-connect.terrapay.com:21211/eig/gsma/reversalInitiate")

https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true

request = Net::HTTP::Post.new(url)
request["X-USERNAME"] = "terrapayuser"
request["X-PASSWORD"] = "101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b"
request["X-DATE"] = "2018-04-04 09:27:16"
request["X-ORIGINCOUNTRY"] = "US"
request["Content-Type"] = "application/json"
request.body = JSON.dump({
  "reversalReason": "reversalreason",
  "txnId": "TPKM000000056269"
})

response = https.request(request)
puts response.read_body

```
> Success Response

```json
{
  "responseMessage": "Reverse Success",
  "statusCode": "16000"
}
```


Reverse Transaction is used to reverse a transfer which is to bring back the money from the beneficiary's account to the sender's account.

<aside class="success">Note :Reversal of transaction is only possible for transaction response code:3000, Transaction Successful.</aside>

### URL
https://uat-connect.terrapay.com:21211/eig/gsma/reversalInitiate/

### HTTP Request
`POST /eig/gsma/reversalInitiate HTTP/1.1`

### Reverse transaction response parameter list
Parameter name |Description |Data Type|Requirement
--------------|------------|-------------|------------
txnId | Reference for the transaction which was returned by transaction response buffer by Terrapay's system or partner transaction id.|String|Mandatory

### Response code for reversal transactions

Response Code | Response Message
-------------|---------------
16000 |Reversal Success.
16001 |Reversal Failed. Transaction Not found.
16002 |Reversal Rejected.
16003 |Reversal Pending.
16004 |Reversal cannot be done at this stage
16005 |Reversal already raised.
16006 |Transaction already reversed.
16007 |Reverse cannot be done. Transaction is in failed state.

## Statements API


```shell-screen-fourteen

```
```javascript-screen-fourteen
```

> Response

```json
[
	{

  		"timestamp": "2020-04-29T13:00:00Z",
		"type": "LIQUIDITY",
		"internalRef": "TP000000000",
		"externalRef": "",
  		"amount": "1000.00",
  		"currency": "USD",
  		"convertedAmount": "",
		"convertedCurrency": "",
		"balance": "1000.00",
		"message": "Transfer with reference 123456"
	},
	{
		"timestamp": "2020-05-22T09:12:42Z",
		"type": "TRANSFERRED",
		"internalRef": "TP000000001",
		"externalRef": "TW000000000",
		"amount": "10.12",
		"currency": "USD",
		"convertedAmount": "38280.09",
		"convertedCurrency": "UGX",
		"balance": "989.88",
		"message": "3000:Remit Success"
	},
	{
		"timestamp": "2020-05-22T10:15:55Z",
		"type": "REJECTED",
		"internalRef": "TP000000002",
		"externalRef": "TW000000001",
 		"amount": "8.62",
		"currency": "USD",
		"convertedAmount": "19938.06",
		"convertedCurrency": "TZS",
 		"balance": "989.88",
		"message": "3007:Beneficiary KYC validation failed"
	},
	{
		"timestamp": "2020-05-22T11:22:45Z",
		"type": "BOUNCED",
		"internalRef": "TP000000003",
		"externalRef": "TW000000000",
		"amount": "10.12",
		"currency": "USD",
		"convertedAmount": "38280.09",
		"convertedCurrency": "UGX",
		"balance": "1000.00",
		"message": "3103:Bank credit failed. Account name mismatch"
	}
]
  ```

### Statement Types
#### TRANSFERRED
Represents successfully transferred transaction. Balance should be deleted

#### REJECTED 
Represents transactions rejected by TerraPay. Balance shouldn't be changed. The reason of the rejection should be populated.

#### BOUNCED
Represents bounced-back transactions. Balance should be credited. Happens when a beneficiary bank returns funds back to TerraPay due to incorrect details, etc.

#### LIQUIDITY
Represents liquidity transactions sent to TerraPay. Balance should be credited.

### Statement fields
Name | Format|Example|Requirement|Description
-------------|---------------|-------------|------|------
timestamp |	ISO 8601 UTC DateTime|2020-04-29T13:00:00Z|Mandatory|	Transaction time
type |TRANSFERRED REJECTED BOUNCED LIQUIDITY| |Mandatory|Transaction time
internalRef|String|TPKM000000056269|Mandatory|TerraPay transaction reference
externalRef|String|88440865645|Optional for LIQUIDITY mandatory for the rest|Partner transaction reference
amount|Decimal|123.45|Mandatory|Transaction amount in balance currency
currency|ISO 4217 three-letter code|USD|Mandatory|Balance currency, USD
convertedAmount|Decimal|	4497.45|Optional for LIQUIDITY mandatory for the rest|Converted amount sent to beneficiary
convertedCurrency|ISO 4217 three-letter code|TZS|Optional for LIQUIDITY mandatory for the rest|Currency of convertedAmount
balance|Decimal|	212455.87|Mandatory|Balance value after the transaction
message|String|3032:Remit Failed.|Mandatory|Extra transaction description should contain parseable reason for REJECTED and BOUNCED type

### Statement's example

Description|TimeStamp|Type|InternalRef|ExternalRef|Amount|Currency|ConvertedAmount|ConvertedCurrency|Balance|Message
----|----|----|---|---|----|----|----|---|----|----
Partner sends funds to TerraPay|2020-04-29T13:00:00Z|LIQUIDITY|TP000000000|  |1000.00|USD|   |  |1000.00|Transfer with reference 123456
Successful transfer for 38280.09 UGX|2020-05-22T09:12:42Z|TRANSFERRED|TP000000001	|	TW000000000|10.12|USD|38280.09|UGX|989.88|3000:Remit Success
Failed transfer for 19938.06 TZS|2020-05-22T10:15:55Z|REJECTED|TP000000002|TW000000001|8.62|USD|19938.06|TZS|989.88|	Transfer with reference 123456
Previously successful transfer to UGX was returned to TerraPay|2020-05-22T11:22:45Z|BOUNCED|TP000000003|TW000000000|10.12|USD|38280.09|UGX|1000.00|3103:Bank credit failed. Account name mismatch


### Request
Statements should be accessible via HTTP GET request.

### Sample URL

### URL
https://uat-connect.terrapay.com:21211/eig/gsma/statements?start=%7Bstart%7D&end=%7Bend%7D¤cy=%7Bcurrency%7D

### Request parameter
Name|Format|Example|Requirement|Description
------|----|---|---|----
start|ISO 8601 UTC DateTime|2020-04-29T13:00:00Z|mandatory|Beginning of the query interval
end|ISO 8601 UTC DateTime|2020-05-22T19:38:59Z|mandatory|End of the query interval

### Request headers
Request must include standard TerraPay headers: 

* X-USERNAME
* X-PASSWORD
* X-DATE
* X-ORIGINCOUNTRY

### Response
Response should contain list of statements in JSON format for the requested period.




## Get Bank List

### Get Bank List <a class="tryitbutton" href='https://developers.terrapay.com/try-it/get-bank-list' target="_blank">Try it </a>

> Get Bank List

```shell-screen-fifteen

curl --location --request GET 'https://connect.terrapay.com:21211/eig/getbanklist/BD'\
--header 'X-USERNAME: username'\
--header 'X-PASSWORD: password'\
--header 'X-DATE:request datetime'\
--header 'X-ORIGINCOUNTRY:origincountry'\
--header 'Content-Type: application/json'
```
```javascript-screen-fifteen
var myHeaders = new Headers();
myHeaders.append("X-USERNAME", "OpenTurfDev");
myHeaders.append("X-PASSWORD", "85d6dcc27d9fb21c7c346cdbcee2b56a84eba0f542a846de06658d2d094afd56");
myHeaders.append("X-DATE", "2018-04-04 09:27:16");
myHeaders.append("X-ORIGINCOUNTRY", "US");

var raw = "";

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("https://uat-connect.terrapay.com:21211/eig/getbanklist/NP", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```
```python-screen-fifteen
import requests

url = "https://uat-connect.terrapay.com:21211/eig/getbanklist/NP"

payload = ""
headers = {
  'X-USERNAME': 'OpenTurfDev',
  'X-PASSWORD': '85d6dcc27d9fb21c7c346cdbcee2b56a84eba0f542a846de06658d2d094afd56',
  'X-DATE': '2018-04-04 09:27:16',
  'X-ORIGINCOUNTRY': 'US'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)

```
```java-screen-fifteen
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
Request request = new Request.Builder()
  .url("https://uat-connect.terrapay.com:21211/eig/getbanklist/NP")
  .method("GET", null)
  .addHeader("X-USERNAME", "OpenTurfDev")
  .addHeader("X-PASSWORD", "85d6dcc27d9fb21c7c346cdbcee2b56a84eba0f542a846de06658d2d094afd56")
  .addHeader("X-DATE", "2018-04-04 09:27:16")
  .addHeader("X-ORIGINCOUNTRY", "US")
  .build();
Response response = client.newCall(request).execute();
```
```ruby-screen-fifteen
require "uri"
require "net/http"

url = URI("https://uat-connect.terrapay.com:21211/eig/getbanklist/NP")

https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true

request = Net::HTTP::Get.new(url)
request["X-USERNAME"] = "OpenTurfDev"
request["X-PASSWORD"] = "85d6dcc27d9fb21c7c346cdbcee2b56a84eba0f542a846de06658d2d094afd56"
request["X-DATE"] = "2018-04-04 09:27:16"
request["X-ORIGINCOUNTRY"] = "US"

response = https.request(request)
puts response.read_body

```
> Success Response

```json
{
	"countryCode": "BD",
	"lastUpdatedOn": "2021-01-12 21:40:00.051",
	"banks": [
	{
		"bankName": "DUTCH BANGLA BANK LIMITED",
		"bankCode": "DBBLBDDH",
		"providerCode": "88090010000",
		"status": "ACTIVE"
	},
	{
		"bankName": "AGRANI BANK LTD",
		"bankCode": "AGBKBDDH",
		"providerCode": "88090030000",
		"status": "ACTIVE"
	},]
}

```	

The Bank list API is used to derive a bank name, code, provider code, and status.


**URI format is**: https://connect.terrapay.com:21211/eig/getbanklist/{countrycode}

<aside class="success">Note: This example is exclusive to Bangladesh.</aside>

### URL
https://connect.terrapay.com:21211/eig/getbanklist/BD
### HTTP Request
`GET /eig/getbanklist/BD HTTP/1.1`

### Bank List request parameter list
Parameter name|Description|Data Type|Requirement|Field Length
---------|--------|--------|--------|------
countryCode|ISO Alpha 2 country code of the destination country. Eg. NG for Nigeria|String|	Mandatory|2
lastUpdatedOn|last updated date and time in YYYY-MM-DD HH:mm:ss.SSS format.|String|Mandatory|22
bankName|Full name of the beneficiary bank|String|Mandatory|4-60
bankCode|Bank Code as required in the destination Country. It can be one of: IFSC Code,Routing Code,Swift BIC. This code is specific to bank integration in each country and may be mandatory in certain destination countries| String|Mandatory|4-25
providerCode|This is a code that indicates the bank to which the transaction is to be sent. If not set, then TerraPay will resolve the bank based on the bankCode. If the bankCode is incorrectly provided, then the bank will be resolved based on Bank Name (should match exactly as per the bank list shared by TerraPay). If these parameters do no match then the transaction will be rejected. If set, then TerraPay will resolve the bank based on the provider code.|Numeric|Conditional|7-12
status|Indicates the status of the account. If 'active' then the account can receive funds. If not then transactions sent to the account will fail.|String|Mandatory|6
