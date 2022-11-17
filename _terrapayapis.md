#TerraPay APIs

This section introduces the set of APIs that are implemented by TerraPay and are available for integration by partners. These APIs cater to the services offered by TerraPay as described above.

The TerraPay APIs are derived from the GSMA API standard. For more detailed information on the GSMA APIs please refer <a href='http://mmapai.gsma.com'>mmapi.gsma.com</a>

Basic Transaction Steps

* Sender initiates a transaction from ,
   * A registered Mobile Wallet
   * An active Bank Account
   * At a MTO agent
* Sender provides the beneficiary mobile number that will receive the funds.
* In case of Remit to Bank, the sender provides the beneficiary bank account details that will receive funds.
* Sending partner forwards the beneficiary mobile number/bank account to TerraPay to validate if the beneficiary can receive funds.
* TerraPay validates if the beneficiary mobile number is associated with a valid payment instrument and if that instrument is active and can receive funds.
* In case of Remit to beneficiary bank account, TerraPay will validate if the bank is supported and the details provided are valid syntactically.
* In addition where ever the receiving partner can provide the beneficiary name, TerraPay does name matching using a propriety fuzzy logic algorithm
* Sender then initiates a quote request. Sender provides the amount to be transferred. TerraPay will process the quote and provide the sender with the foreign exchange rate and the amount the beneficiary will receive.
* Sender then confirms the transaction.
* TerraPay validates the transaction and credits the amount to beneficiary mobile number or bank account


<aside class="notice">
**NOTE- Both sender and beneficiary KYC has to be provided by the sending and receiving partners to TerraPay in order to perform sanctions screening and AML/CFT validations. This information is mandatory and has to be provided via the API calls.
</aside>
**NOTE**:
All API calls to the TerraPay Network should include the following HTTP Headers

`X-USERNAME: "partnerUserName"`

`X-PASSWORD: "partnerPassWord"`

`X-DATE: "YYYY-MM-DD HH:mm:ss"`

`X-ORIGINCOUNTRY: "Country Code in which the transaction is created. ISO Alpha 2 standard"`

X-USERNAME, X-PASSWORD values will be shared with the Partner during the on boarding process on test and production environments separately.
Username and Password is always case-insensitive.

X-PASSWORD must be SHA256 hash encoded when sent over the API request.`
