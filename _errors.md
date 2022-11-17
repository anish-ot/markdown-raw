# Errors


The TerraPay API uses the following error codes:


Error Code | Meaning
---------- | -------
1000 | Invalid [propertyName] -- Check for invalid request parameter(s).
1001 | [propertyName] value should be between [minlength] to [maxlength] -- Check for invalid request parameter(s)
1002 | [propertyName] must be [length] -- Check for invalid request parameter(s)
1003 | Authentication failed. Username or Password is incorrect. -- Contact TerraPay operations team for valid username and password.
1004 | Invalid parameters in the request -- Check for invalid request parameter(s).
1005 | Mandatory fields are missing	-- Check for invalid request parameter(s).
1006 | Request SHA256 checksum mismatch	-- Check for invalid checksum sent with request.
1007 | Server is busy.Please try after sometime	-- Failure due to network issues or unhandled exceptions.
1010 | Source country not allowed -- Operation team needs to check source country configuration.
1011 | Destination country not allowed	 --	Operation team needs to check destination country configuration.
1012 | Source currency not allowed	-- Operation team needs to check source currency configuration.
1013 | Destination currency not allowed	-- Operation team needs to check destination currency configuration.
1014 | Source country inactive	-- Operation team needs to check source country configuration.
1015 | Destination country inactive	-- Operation team needs to check destination country configuration.
1016 | Failed to get destination partner	-- Operation team needs to check corridor configuration.
1017 | Source partner validity fail	--	operations team needs to extend validity of source partner in system.
1018 | Destination partner validity fail -- operations team needs to extend validity of destination partner in system.
1019 | Source partner suspended	-- operations team needs to check activation status of partner.
1020 | Destination partner suspended	--	operations team needs to check activation status of partner.
1021 | Source partner inactive	--	operations team needs to check activation status of partner.
1022 | Destination partner inactive	 --	operations team needs to check activation status of partner.
1023 | Corridor validity failed	 --	operations team needs to check corridor validity.
1024 | Corridor Suspended	 --	operations team needs to check corridor activation status.
1026 | Source MSISDN not allowed. --	Invalid source/sender's mobile number.
1027 | Source MSISDN Blacklisted. --	Source/sender's mobile number is black listed.
1028 | Destination MSISDN not allowed. --	Invalid destination mobile number.
1029 | Destination MSISDN Blacklisted. --	Destination mobile number is black listed.
1030 | Corridor not exists  --	Operation team needs to check corridor configuration.
1031 | Source currency inactive	 --	Operation team needs to check currency configuration.
1032 | Destination currency inactive	 --	Operation team needs to check currency configuration.
1046 | Invalid Transaction ID.	-- Check for transaction Id format (special characters).
1061 | Destination Country Sanctioned. -- Destination country is on sanction list . Transaction cannot be delievered.
1062 | Source Country Sanctioned. -- Source country is on sanctionlist. Transaction cannot be delievered.
1073 | Routing Failed.	--	Route is inactive. Check with TerraPay operations team to enable the route and retry.

