# Authentication

> To authorize, use this code 

```shell 
  curl --location --request GET 'API_ENDPOINT' \
--header 'X-DATE: 2020-01-02 10:51:16' \
--header 'X-ORIGINCOUNTRY: US' \
--header 'X-USERNAME: PARTNER_USERNAME' \
--header 'X-PASSWORD: PARTNER_PASSWORD' \
--header 'Content-Type: application/json'
```

```javascript
```

> Make sure to replace headers with your username and password

All API calls to the TerraPay Network should include the following HTTP Headers

`X-USERNAME: "partnerUserName"`

`X-PASSWORD: "partnerPassWord"`

`X-DATE: "YYYY-MM-DD HH:mm:ss"`

`X-ORIGINCOUNTRY: "Country Code in which the transaction is created. ISO Alpha 2 standard"`

X-USERNAME, X-PASSWORD values will be shared with the Partner during the on boarding process on test and production environments separately.
Username and Password is always case-insensitive.
X-PASSWORD must be SHA256 hash encoded when sent over the API request.`


<aside class="notice">
You must replace <code>partnerUserName</code>  and <code>partnerPassWord</code>with your partner details.
</aside>

 