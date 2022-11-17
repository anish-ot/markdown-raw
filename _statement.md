# Statements 
## Statements API
```shell

```
```javascript
```

> Response

```json
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
  ```

### Statement Types
### TRANSFERRED
Represents successfully transferred transaction. Balance should be deleted

### REJECTED 
Represents transactions rejected by TerraPay. Balance shouldn't be changed. The reason of the rejection should be populated.

### BOUNCED
Represents bounced-back transactions. Balance should be credited. Happens when a beneficiary bank returns funds back to TerraPay due to incorrect details, etc.

### LIQUIDITY
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
Description|Timestamp|Type|InternalRef|ExternalRef|Amount|Currency|Converted Amount|Converted Currency|Balance|Message
----|----|----|---|---|----|----|----|---|----|----
Partner sends funds to TerraPay|2020-04-29T13:00:00Z|LIQUIDITY|TP000000000|  |1000.00|USD|   |  |1000.00|Transfer with reference 123456
Successful transfer for 38280.09 UGX|2020-05-22T09:12:42Z|TRANSFERRED|TP000000001|TW000000000|10.12|USD|38280.09|UGX|989.88|3000:Remit Success
Failed transfer for 19938.06 TZS|2020-05-22T10:15:55Z|REJECTED|TP000000002|TW000000001|8.62|USD|19938.06|TZS|989.88|	Transfer with reference 123456
Previously successful transfer to UGX was returned to TerraPay|2020-05-22T11:22:45Z|BOUNCED|TP000000003|TW000000000|10.12|USD|38280.09|UGX|1000.00|3103:Bank credit failed. Account name mismatch

### Request
Statements should be accessible via HTTP GET request.

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

