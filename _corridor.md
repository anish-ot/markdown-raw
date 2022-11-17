# Corridor Quotation
## Corridor Quotation 
```shell
curl --location --request GET'https://uat-connect.terrapay.com:21211/eig/gsma/quotations/all '\
--header 'X-USERNAME: partneruat'\
--header 'X-PASSWORD: 101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b'\
--header 'X-DATE: 2017-05-03 11:00:00'\
--header 'X-ORIGINCOUNTRY:US'\
--header 'Content-Type: application/json'
```
```javascript
```
> Success Response

```json
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
```


This API is used to get the foreign exchange rates for all the corridors that are active for the partner.


**URI format is:** /quotations/all


### HTTP Request
`GET https://uat-connect.terrapay.com:21211/eig/gsma/quotations/all`

