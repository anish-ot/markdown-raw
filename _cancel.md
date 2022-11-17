# Cancel Transaction
## Cancel Transaction
```shell
curl --location --request POST 'https://uat-connect.terrapay.com:21211/eig/gsma/remitCancel/'\
 --header 'X-USERNAME: partneruat'\
 --header 'X-PASSWORD: 101dfd2422f23f06120b77ab17d39229ff9bb40563eae042bc6cc6e8f9f1825b'\
 --header 'X-DATE: "2021-01-03 11:00:00'\
 --header 'X-ORIGINCOUNTRY:US'\
 --header 'Content-Type: application/json'\
 --data-raw
   {
        "cancelreason": "cancelling",
        "txnId": "TPSE000000298941"
   }
 
```

```javascript
```

> Success Response

```json
{
  "responseMessage": "Cancel Success",
   "statusCode": "15000"
 }
```

This API is used to cancel an initiated transaction which is not yet credited. The cancellation will be done only if the transaction is pending on the TerraPay system and has not already been sent to the receiving partner for credit to the beneficiary account

### HTTP Request

`POST https://uat-connect.terrapay.com:21211/eig/gsma/remitCancel/`

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


