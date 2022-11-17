# Bank List

## Get Bank List

```shell

curl --location --request GET 'https://connect.terrapay.com:21211/eig/getbanklist/BD'\
--header 'X-USERNAME: username'\
--header 'X-PASSWORD: password'\
--header 'X-DATE:request datetime'\
--header 'X-ORIGINCOUNTRY:origincountry'\
--header 'Content-Type: application/json'
```
```javascript
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
	},
	{
		"bankName": "COMMUNITY BANK",
		"bankCode": "COYMBDDD",
		"providerCode": "88090600000",
		"status": "ACTIVE"
	}			
  ]
}

```	

The Bank list API is used to derive a bank name, code, provider code, and status.


**URI format is**: https://connect.terrapay.com:21211/eig/getbanklist/{countrycode}

<aside class="success">Note: This example is exclusive to Bangladesh.</aside>
### HTTP Request
`GET https://connect.terrapay.com:21211/eig/getbanklist/BD`

### Bank List request parameter list
Parameter name|Description|Data Type|Requirement|Field Length
---------|--------|--------|--------|------
countryCode|ISO Alpha 2 country code of the destination country. Eg. NG for Nigeria|String|	Mandatory|2
lastUpdatedOn|last updated date and time in YYYY-MM-DD HH:mm:ss.SSS format.|String|Mandatory|22
bankName|Full name of the beneficiary bank|String|Mandatory|4-60
bankCode|Bank Code as required in the destination Country.This code is specific to bank integration in each country and may be mandatory in certain destination countries| String|Mandatory|4-25
providerCode|This is a code that indicates the bank to which the transaction is to be sent. If not set, then TerraPay will resolve the bank based on the bankCode. If the bankCode is incorrectly provided, then the bank will be resolved based on Bank Name (should match exactly as per the bank list shared by TerraPay). If these parameters do no match then the transaction will be rejected. If set, then TerraPay will resolve the bank based on the provider code.|Numeric|Conditional|7-12
status|Indicates the status of the account. If 'active' then the account can receive funds. If not then transactions sent to the account will fail.|String|Mandatory|6

