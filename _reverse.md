```shell
curl --location --request POST 'https://uat-connect.terrapay.com:21211/eig/gsma/reversalInitiate/'\
--header 'X-USERNAME: partneruat'\
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
```javascript
```
> Success Response

```json
{
  "responseMessage": "Reverse Success",
  "statusCode": "16000"
}
```


Reverse Transaction is used to reverse a transfer which is to bring back the money from the beneficiary's account to the sender's account.

<aside class="success">Note :Reversal of transaction is only possible for      transaction response code:3000, Transaction Successful.</aside>

### HTTP Request
`POST https://uat-connect.terrapay.com:21211/eig/gsma/reversalInitiate/`

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

