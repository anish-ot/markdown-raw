# Ledger Balance

The ledger balance API is used for get the current balance in the partner's ledger. The balance can be retrieved for a particular currency ledger or all currencies ledger. The ledger balance is retrieved only if the ledger is active. 

**URI format is:** accounts/{currency}/balance

## Get Balance of all ledgers
```shell
curl --location --request GET 'https://uat-connect.terrapay.com:21211/eig/gsma/accounts/all/balance'\
--header 'X-USERNAME: partneruat'\
--header 'X-PASSWORD: 101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b'\
--header 'X-DATE: 2017-05-03 11:00:00'\
--header 'X-ORIGINCOUNTRY:US'\
--header 'Content-Type: application/json '
```

```javascript
```

>  Success Response: 


```json
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
```


### HTTP Request
`GET https://uat-connect.terrapay.com:21211/eig/gsma/accounts/all/balance`

## Get Balance for a single currency ledger
```shell
curl --location --request GET 'https://uat-connect.terrapay.com:21211/eig/gsma/accounts/USD/balance'\
--header 'X-USERNAME: partneruat'\
--header 'X-PASSWORD: 101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b'\
--header 'X-DATE: 2017-05-03 11:00:00'\
--header 'X-ORIGINCOUNTRY:US'\
--header 'Content-Type: application/json'
```
```javascript
```
> Success Response: 


```json
{
		"currency": "USD",
		"currentBalance": "1000.000000",
		"status": "available"
	}
	
```

### HTTP Request
`GET https://uat-connect.terrapay.com:21211/eig/gsma/accounts/USD/balance`

