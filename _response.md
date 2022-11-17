# Response Codes & Messages
## Generic Response
### Generic Response Code & Messages
Response Code|Response Message|	Contact TerraPay|Transaction Action|Remarks/Comments
----|----|----|----|----
1000|Invalid [propertyName]|No|	Retry|	Check for invalid request parameter(s)
1001|[propertyName] value should be between [minlength] to [maxlength]|	No|	Retry|	Check for invalid request parameter(s)
1002|[propertyName] must be [length]|No	|Retry|Check for invalid request parameter(s)
1003|Authentication failed. Username or Password is incorrect.|	Yes|Retry|Contact TerraPay operations team for valid username and password.
1004|Invalid parameters in the request|No|	Retry|Check for invalid request parameter(s).
1005|Mandatory fields are missing|No|Retry|	Check for invalid request parameter(s).
1006|Request SHA256 checksum mismatch|No|Retry|Check for invalid checksum sent with request.
1007|Server is busy.Please try after sometime|Yes|Retry|Failure due to network issues or unhandled exceptions.
1010|Source country not allowed|Yes|Retry|Operation team needs to check source country configuration.
1011|Destination country not allowed|Yes|Retry|	Operation team needs to check destination country configuration.
1012|Source currency not allowed|Yes|Retry|	Operation team needs to check source currency configuration.
1013|Destination currency not allowed|Yes|	Retry|Operation team needs to check destination currency configuration.
1014|Source country inactive|Yes|Retry|	Operation team needs to check source country configuration.
1015|Destination country inactive|Yes|Retry|Operation team needs to check destination country configuration.
1016|Failed to get destination partner|Yes|Retry|Operation team needs to check corridor configuration.
1017|Source partner validity fail|Yes|Retry|operations team needs to extend validity of source partner in system.
1018|Destination partner validity fail|	Yes|Retry|operations team needs to extend validity of destination partner in system.
1019|Source partner suspended|Yes|Retry|operations team needs to check activation status of partner.
1020|Destination partner suspended|Yes|Retry|operations team needs to check activation status of partner.
1021|Source partner inactive|Yes|Retry|operations team needs to check activation status of partner.
1022|Destination partner inactive|Yes|Retry|operations team needs to check activation status of partner.
1023|Corridor validity failed|Yes|Retry|operations team needs to check corridor validity.
1024|Corridor Suspended	|Yes|Retry|operations team needs to check corridor activation status.
1026|Source MSISDN not allowed.|No|	Cancel|	Invalid source/sender's mobile number.
1027|Source MSISDN Blacklisted.|No|	Cancel|	Source/sender's mobile number is black listed.
1028|Destination MSISDN not allowed.|No	|Cancel	|Invalid destination mobile number.
1029|Destination MSISDN Blacklisted.|No|Cancel|	Destination mobile number is black listed.
1030|Corridor not exists|Yes|Retry|	Operation team needs to check corridor configuration.
1031|Source currency inactive|Yes|Retry|Operation team needs to check currency configuration.
1032|Destination currency inactive|Yes|	Retry|Operation team needs to check currency configuration.
1046|Invalid Transaction ID.|No|Retry|Check for transaction Id format (special characters).
1061|Destination Country Sanctioned.|No	|Cancel|Destination country is on sanction list.Transaction cannot be delievered.
1062|Source Country Sanctioned.|No|Cancel|Source country is on sanctionlist. Transaction cannot be delievered.
1073|Routing Failed.|Yes|Retry|	Route is inactive.Check with TerraPay operations team to enable the route and retry.

## Beneficiary Validation Responses
### Beneficiary Validation Responses Codes & Messages
Response Code|Response Message|Contact TerraPay|Transaction Action|Remarks/Comments
-----|-----|-----|-----|-----
6000|Beneficiary MSISDN Validation Success|No|No|Transaction validation is success.
6001|Corridor does not exists|Yes|Retry	|Operation team needs to check the corridor configuration.
6002|Corridor inactive|	Yes|Retry|Operation team needs to check the corridor configuration.
6003|Beneficiary MSISDN blacklisted|No|Cancel|Beneficiary MSISDN has been blacklisted on TerraPay system..
6004|Beneficiary validation failed|	Yes|Cancel|Operation team needs to check.
6005|Beneficiary Registered but not KYCed|No|Cancel|Beneficiary is registered with destination partner network with incomplete KYC details.
6006|Beneficiary MSISDN not found|No|Cancel	|Beneficiary is not registered with destination partner network.
6007|Beneficiary Suspended|No|Cancel|Beneficiary is in suspended state on TerraPay system.
6008|Beneficiary name does not match|No|Cancel|	Beneficiary validation failed.
6009|Beneficiary validation failed. Request timed out at destination partner|Yes|	Retry|Operation team needs to check the time out issue.
6010|Mandatory KYC parameter check failed|Yes|Retry|Resend the transaction with required KYC parameters.
6011|Validation Failed. Beneficiary must register or upgrade KYC Level to receive transactions|No|Cancel|Beneficiary validation failed.
6012|Beneficiary KYC Verification Pending|No|Cancel	|Beneficiary validation failed.
6013|Receiver Name Missing|	No|Cancel|	Beneficiary validation failed.
6014|Customer Not Registered|No|Cancel|	Beneficiary validation failed.
6017|Beneficiary Account is locked|	No|	Cancel|	Beneficiary validation failed.
6019|Destination Partner Timed Out - Please retry.|	Yes|Retry|Operation team needs to check time out issue.
6022|Beneficiary Account Inactive|No|Cancel|Beneficiary validation failed.
6020|Beneficiary Account is Inactive|No|Cancel|	Beneficiary validation failed.
6101|Destination bank not configured|Yes|Retry|	Operation team needs to check configuration.
6102|Invalid Bank Account Number|No|Cancel|	Send the transaction with valid account number.
6103|Destination bank not reachable|Yes|Retry|Operation team needs to check.
6104|Validation Failed at Destination Partner|Yes|Retry|Operation team needs to check.
6023|Provider code is missing|No|Cancel|Send the transaction with valid provider code.
6024|Provider code does not match operator network|	No|	Cancel|	Send the transaction with valid provider code.

## Quote Response
### Quote Response Codes & Messages
Response Code|Response Message|	Contact TerraPay|Transaction Action|Remarks/Comments
------|-------|-----------|-------|--------
2000|Quote Success|	No|	No|	Quotation is success.
2001|Source amount is invalid|	No|	Retry|	Send correct/valid source amount with quote request.
2002|Beneficiary MSISDN validation failed|No|Cancel|Beneficiary validation is in failure state for which quote request is initiated.
2003|Failed to get Forex rate|Yes|Retry|Operation team needs to check rate configuration.

## Remit Response
### Remit Response Codes & Messages


Response Code|Response Message|Contact TerraPay|Transaction Action|Remarks/Comments
------|--------|---------|-----|-------
3000|Remit Success|No|No|Transaction is in success state.
3050|Remit Acknowledged, status PENDING|No|	Poll|Partner needs to poll status API till transaction status changes to success/failed.
3001|Transaction request should be current date.|No|Retry|Transaction request should be current date.
3002|Beneficiary Validation failed|No|Cancel|Beneficiary validation is in failure state for which remit request is initiated.
3003|TerraPay transaction id is invalid|No|Retry|Retry transaction with valid TerraPay transaction id.
3004|Duplicate transaction Id|No|Cancel|Send transaction with unique transaction/reference id.
3005|Quote and Remit parameters do not match|No|Retry|Send the parameters as per API specification.
3006|Sender KYC validation failed|No|Cancel|Transaction is failed.
3007|Beneficiary KYC validation failed|No|Cancel|Transaction is failed.
3008|Quote expired|No|Cancel|Initiate a new a quote request and send new quote reference with remit request.
3009|Failed to process quote request|Yes|Retry|Operation team needs to check.
3010|Mandatory KYC parameter check failed|No|Retry|Check for sender's KYC parameters in remit request.
3011|Invalid Fx Rate|Yes|Retry|	Check with TerraPay operations on the Fx rate configuration.
3022|Corridor validation failed	|Yes|Retry|	Operation team needs to check the corr configuration.
3027|Server is busy. Please try after sometime|Yes|	Retry|Check with TerraPay technical team before retry.
3030|Possible duplicate transaction received within configured time.|Yes|Retry|Wait for sometime and send the transaction again.
3031|Connection timeout while connecting to destination partner|Yes|Retry|Wait for sometime and send the transaction again.
3032|Remit failed|Yes|Cancel|Operation team needs to check logs and update.
3049|Remit Failed. Insufficient funds|No|Retry|Check your balance at TerraPay and retry after balance is funded.
3060|Beneficiary daily transaction count limit reached|No|Cancel|Beneficiary has reached the daily transaction count.
3061|Beneficiary weekly transaction count limit reached|No|Cancel|Beneficiary has reached the weekly transaction count.
3062|Beneficiary monthly transaction count limit reached|No	|Cancel|Beneficiary has reached the monthly transaction count.
3072|Receiver Daily Transaction Limit Reached|No|Cancel|Beneficiary daily transaction limit has reached.
3075|Sending Partner Min allowed amount check failed.|No|Cancel|Sending partner is sending less than minimum confiured transaction amount.
3076|Sending Partner Max allowed amount check failed.|No|Cancel|Sending partner is sending more than maximum configured transaction amount.
3077|Receiving Partner Min allowed amount check failed.|No|Cancel|Receiving partner is receiving less than minimum confiured transaction amount.
3078|Receiving Partner Max allowed amount check failed.|No|Cancel|Receiving partner is receiving more than maximum confiured transaction amount.
3079|Sender Min allowed amount check failed.|No|Cancel|Sender is sending less than minimum confiured transaction amount.
3080|Sender Max allowed amount check failed.|No|Cancel|	Sender is sending more than maximum confiured transaction amount.
3081|Receiver Min allowed amount check failed.|No|Cancel|Beneficiary is receiving less than minimum confiured transaction amount.
3082|Receiver Max allowed amount check failed.|No|Cancel|Beneficiary is receiving more than maximum confiured transaction amount.
3100|Credit Failed. Msisdn not found.|No|Cancel	|Transaction has failed due to invalid wallet account.
3101|Bank Credit Failed. Invalid Account.|No|Cancel|Transaction has failed by bank due to invalid bank account.
3102|Bank Credit Failed. Bank Not Reachable.|No|Cancel|Transaction failed by destination partner as bank is not reachable.
3103|Bank credit failed. Account name mismatch.|No|Cancel|Transaction failed by bank due to account name mismatch.
3104|Bank credit failed. Transaction limit exceeded.|No|Cancel|Transaction failed by bank as transaction limit exceeded.
3105|Bank credit failed. Transaction not permitted.|No|	Cancel|	Transaction failed by bank as transaction is permitted.
3106|Bank credit failed. Unknown Error.|Yes|Retry/Cancel|As the transaction failed by bank, please check with operations team either transaction can be retried or not.
3107|Invalid Amount Limit.|	No|	Cancel|Transaction failed due to max limit per transaction.
3108|Invalid Digital Signature.|Yes|Cancel|Transaction has failed due to account not registed.
3109|Insufficient funds in the receiving partner account.|Yes|Cancel|Operation team needs to check the prefunding balance.
3110|Invalid Beneficiary Account|Yes|Cancel|Transaction has failed due to invalid account.
3111|Beneficiary Account not Registered|Yes|Cancel|Transaction has failed due to account not registed.
3112|Duplicate VendorId	|No|Cancel|Send the correct vendorID.
3113|Beneficiary Account Limit Reached.|No|	Cancel|Transaction failed due to transaction limit exceeded.
3114|Beneficiary Account Barred.|No|Cancel|Transaction failed as account is Barred.
3115|Beneficiary Account Inactive|No|Cancel|Transaction failed as account is inactive.
3116|Beneficiary Account Locked|No|Cancel|Transaction failed as account is locked.
3117|Transfer type not supported|No|Cancel|Please check the transfer type and retry the transaction with the correct Transfer type
3132|Remit Failed - Max retry limit reached.|No|Cancel|Transaction failed as transaction limit exceeded.
3222|Invalid UPI amount.|No|Cancel|	The provided amount is not acceptable for UPI transaction.