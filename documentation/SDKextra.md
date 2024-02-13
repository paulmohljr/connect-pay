# Extra Information from SDK. Not sure if needed. 
This was information from section 4.2
## Sample JSON Response for SDK
```json
{
"componentDelta": "responseDataEncryptedUsingAESKey" 
"componentFallBack": "{string}"
}
```

## Response Data Elements Specification for SDK

|Data Element|Description|Requires Encryption| Required?| Rules|Data Type| Minimum Length| Maximum Length|#Occur|
|------------|-----------|-------------------|----------|------|---------|---------------|---------------|------|
|componentDelta|Encrypted Response Payload|Y|O||||||
|componentFallBack|This would only be populated if decryption failed on ConnectPayAPI because SDK sent details which resulted in decryption exception. This would be clear error response payload which signifies decryption error.|N|O||||||

## Decrypted Component Delta JSON format for SDK
```json
{
"transactionStatus": "{string}", 
"transactionStatusCode": "{string}", 
"referenceTransactionID": "{string}", 
"transactionStatusDescription": "{string}", 
"responseVerbiage": "{string}",
"nonce": "{string}",
"errorDetails": [
{
"errorCode": "{string}",
"errorField": "{string}",
"errorReason": "{string}"
}
],
"account": [
{
"userDetails": {
"firstName": "{string}",
"lastName": "{string}",
"email": "{string}"
},
"userAddressDetails": {
"street": "{string}",
"street2": "{string}",
"state": "{string}",
"city": "{string}",
"postalCode": "{string}"
},
"userIdentificationDetails": { 
"routingNumber": "{string}", 
"accountNumber": "{string}", 
"onlineBankTransactionId": "{string}"
},
"userPhone": [
{
"number": "{string}"
}
]
}
],
" teleCheckDetails ": { 
"transactionId": "{string}", 
"tckResponseCode": "{string}", 
"approvalCode": "{string}", 
"denialRecordNumber": "{string}", 
"displayText": "{string}", 
"sequenceId": "{string}", 
"ecaOfferCode": "{string}", 
"achTransactionStatus": "{string}", 
"amount": "{string}",
"currency": "{string}", 
"responseMessageMisc": "{string}", 
"dateTime": "{string}", 
"returnCheckFee": "{string}", 
"returnCheckNote": "{string}",
"key": "{string}",
"accessId": "{string}",
"merchantId": "{string}", 
"description": "{string}", 
"merchantReference": "{string}", 
"paymentType": "{string}",
"returnUrl": "{string}",
"cancelUrl": "{string}", 
"requestSignature": "{string}", 
"onlineBankTransactionId": "{string}" },
"partner": {
"subscriberID": "{string}" },
"customer": {
"fdCustomerID": "{string}", 
"externalID": "{string}"
},
"security": {
"tokenID": "{string}", 
"issuedOn": "{timestamp}", 
"expiresInSeconds": "{number}", 
"publicKey": "{string}", 
"alogorithm": "{string}",
"status": "{string}"
}
}
```

## Create Session Token
>Note: This is a re-write from SDK guide. I do not think this is needed if we can just call the API. 
<p>
The Create Session Token API call is used to create a session token and to retrieve the public encryption key generated for this session. This information will be used to initialize the ConnectPay SDK for every use case. This API is secured as it requires the Authorization header that can only be derived using the API Secret stored in the Merchant’s web server. Below are the details of the API end point.
</p>

## Connectivity
|Attribute|Value|
|---------|-----|
|Cert  API Endpoint | https://cat.api.firstdata.com/gateway/v2/connectpay/security/createsessiontoken|
|Production  API Endpoint | https://prod.api.firstdata.com/gateway/v2/connectpay/security/createsessiontoken|

## Header Description
|Headers|Description|
|-------|-----------|
|Content-Type|application/json|
|Api-Key|Merchant’s ConnectPay FirstAPI key|
|Timestamp|Request initiation timestamp, expecting Epoch time. The value has to generate out of UTC timestamp and it is in milliseconds. Sample value format is 1499961987232|
|Authorization|HMAC for Authenticating Merchant with ConnectPay on FirstAPI, and Authorizing to process business functionality Value for this header should be the word HMAC, followed by a space, followed by values for computed HMAC. Example : HMAC G9FqRSvZGMuJbjgLovkdlYz9ppBGh0++/5d/BIwoUuE= |

### Request Body
<p>
This is the only request where payload is not encrypted, since this call is requesting the Public Encryption Key to encrypt subsequent calls.
</p>
<p>
Sample request body for CreateConsumerProfile, ConsumerEnrollment, AccountValidations, GetConsumerAccountDetails, GetConsumerAccountList, ACH Transaction calls:
</p>

```json
{
    "security": {
      "publicKeyRequired": "true" 
    }
}
```
Sample request body for MicroDepositValidation, ConsumerUpdates and ACH account closure:
```json
{
    "account": [
      {
        "fdAccountID": "CP1GWQ1571349549912484x2r1yf", 
        "type": "ACH"
      }
      ], 
      "security": {
        "publicKeyRequired": "true" 
    }
}
```
|Data Element|Description|Requires Encryption|Required?|Rules|Data Type|Minimum Length|Maximum Length|# Occur|
|------------|-----------|-------------------|---------|-----|---------|--------------|--------------|-------|
|fdAccountID|fdAccountID is required for MicroDepositValidation , ConsumerUpdates and ACH account closure calls|N|C||A,N|1|50|<=1|
|type|Defines the account type for this request.Should always be **ACH**. This element should be present if account section is present|N|C||A|3|3|1|
|publicKeyRequired|Specifies if a public key is required in response.Allowable values for this field are either **true** or **false**|N|Y||A|4|5|1|



### Response Body
<p>Create session token response would contain the response in unencrypted / clear / readable format.</p>
<p>RSA public key from the response of this call would be used to encrypt the AES key and IV for the subsequent calls.</p>
<p>Until the end of this call we would not have all the necessary pieces of information for doing a full payload encryption / decryption</p>
<p>Sample response body for CreateSessionToken call</p>

```json
{
"transactionStatus": "APPROVED",
"transactionStatusCode": 0,
"referenceTransactionID": "ee5870a4-b5a4-3cc8-89da-e67f30c6628c", "transactionStatusDescription": "OK",
"security": {
"tokenID": "0zdH0UyzmQN9m2zbYsFmm0MS4jgd", "issuedOn": "1571430030138",
"expiresInSeconds": "599",
"publicKey":
"MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAs+OzWu916RvgPWkqXN79onLlMlSwIp0P WylPshXhybp/127cvPNblbzq3dIOysGHZK8ZNVjYA5qETmE98wLqM/msBepdslnjj9Z6DNiDruQo4K6L6 EV7K8Nz258ZE6OgBoixy5ZQDFgIgzlpGfEmgQrfG0CiFe7oeC8BXRyWlZNJjvf0ya7Wn/UN5cM8qpf1lR0 ySJTWcxsQz1qSMRB5KEtQjz/Yyj9f9YyvvNCn/aCg45ydKcrGSCpfeLQtsCknviukcsudmBFbJtsTKUjPQ deuUCy4ToD2lKdwQmE+cZQG/FvAVM1MFvK65q6N5TaTx1a6RGfxP5WyKDcHQZDS3QIDAQAB",
"algorithm": "RSA/None/PKCS1Padding",
"status": "ACTIVE" }
}
```
<p>The Create Session Token API call is used to create a session token and to retrieve the RSA public key. This API is secured as it requires the Authorization header that can only be derived using the API Secret stored in the Merchant’s server. Below is more information on the API specification as well as example request and response payloads. </p>

Try it below to also see acceptable error and acceptance codes: 
[![](/assets/images/button.png '')](https://qa-developer.fiserv.com/product/ConnectPay/api/?type=post&path=/security/createsessiontoken&branch=develop&version=1.0.0)


!-- Already in the request section of guide
<p>
Headers|Description|
|---------|-----|
|Content-Type|application/json|
|Api-Key|Merchant’s ConnectPay FirstAPI key|
|Timestamp|Request initiation timestamp, expecting Epoch time. The value has to generate out of UTC timestamp and it is in milliseconds. Sample value format is 1499961987232|
|Authorization|HMAC for Authenticating Merchant with ConnectPay on FirstAPI, and Authorizing to process business functionality.
Value for this header should be the word HMAC, followed by a space, followed by values for computed HMAC. Example : HMAC G9FqRSvZGMuJbjgLovkdlYz9ppBGh0++/5d/BIwoUuE= |
|Client-Token |Session Token received from CreateSessionToken call. Value for this header should be Bearer, followed by a space, followed by values for tokened. Example: Bearer b361Nhsd97hsujuiUSuiua99iq9921kkjsuuahjsa | 
</p>
<br>

<p>Request Body: (Sample request body before payload encryption) </p>
<!-- Already in API Explorer>
```json
{
"customer": {
"externalID": "Merchant01Consumer65746635" }
}
```
<!-- Need to move this requirements information to API explorer. This table is not needed. 

|Data Element|Description|Requires Encryption|Required?|Rules|Data Type|Minimum Length|Maximum Length| #occur|
|------------|-----------|-------------------|---------------|---------|--------------|--------------|-------|
|externalID|This is the user’s unique identifier in the merchant system.|N|R||A,N|1|50|<=1|
-->


<p>Sample request body after payload encryption and before transmission</p>
<!-- added to examples>
```json
{
"componentX":
"L0WLCiqw0TT0tqaRH3Ksz4wdQFf2YAnIeiCScd+hrAWO2Hlv7lDsNnQpd+ORxkIjOHmwJuC58Q0tsc WnOI2Gh5DJ75wk5xnp/0RWQoB2+pTMGo6On+O+vFxkhVQRKlRgJu0G/RNZV4EFa1iBdDTY6UZL0I WtqDT1zwUiu+2NWAOdPDIbAIsekhJrhRAIFNsHeiYhUxBCsF+gxybJupB0XjGIWhAkPjO7AKPR1fXWU/ ZRifzsdu1/X43DSTz4d4/bYAD6iAaSBJUewSVwUG9OodeU84LYgdba4vRNa2G3BpzfomdvK6H1C8pj HjnVjUGP2F3IO6tMDnpAFZfrxvytlg==",
"componentY": "K5BTgBGzhIux2ZnodU4MWRUVhUFbU4P376TLTHZa02nU2jVb2pAWK3gMfpEHsE7WeoLlNrzAJwR 1FJ679z4Oo/yWp7k39zamQNlMHvm6EYBBbxIemexBHIIqqNRFdHhq6S3pA6L/9ItyscEl5/zZIKxcx44hv CCPZOZUhnOTSc4ehPnYJhdJQFgIDhY5UPRRZntM8hP2hOPZTVz5D4re17bSYVOEEK7bmpGIWpf9p ERUj4MlUpyRpafNd2mQsZpXPvW3XZfHDbslO7o3LourFHRSqAfBHOfx+pwH+YcMwglnay/Ay2SYWyZ hKkD+UcHSkyBdk/AMdcKt1K9uCIPm/Q==",
"componentDelta": "KKRKg/jPcb+r/3TZmhLP/KxrMEajXKvBYQd5jeGFm2OzznUvNHuyEhWyJc4RlXFRoLhwcj9eEuSOz0a bTAeU+Xw8hSMJ6kYhHokJ3ev8tgQ="
}
```
-->

<!-- Already in API explorer
<p>In either case, the decrypted/unencrypted version of this payload has three high level transactionStatus , namely, APPROVED/DECLINED/ERROR.</p>

**APPROVED** as the name suggests represents a successful outcome.
<br>

**DECLINED** status signifies that ConnectPayAPI rejected the request either due to format validation or business validation.
<br>

**ERROR** status signifies a system error or equivalent.
<br>
-->

### Request Body after payload encryption and before transmission
For a sample request body **AFTER** payload encryption and before transmission: 
```json
{
    "componentX": "ju5PPi7k4K2jtI0z47qKcHnQGRrIymN+dK+PVlWjKyufoaUHJqjqOAbjsQZ0q3sLciBkEVWm5jGbWQoGf2e9Us+yfYu8ua2hz3wOIRSymHdx8qKuoexQiKhLWnp/GAL0+TIdzb/CvNijuJkOe1XSzEoFdFjYgRNMV8LJM3G/izn48kZm9gexM/iJenJyzwFoqXJc7EcWrC3C0RlkBF5jTgZzTGCvBpxDq4pw3CjFDsGvFy5Gg26B1KRcRDctrFpLV697QAW//hWyS91NYB68S3TIo/B6/LfUjj9bOY3fM+i+5BY2oV7zbLLyvA+CKfLFRBoXtevfBJyndrUDFD0EBA==",
    "componentY": "CqTTfUbNR66rGRhAKGqnEYJBGona07l2lvV7s7sEG97b0eohkWCqcw/XhCSy2+A6rYxhhuvvQ+orjfmCzssIl4Uz+4gu3GE3lfMGeykjRuhipyV+fjnjOBcw/VDOg3IXffr4Oe/isRYTZ5gp0uht89Rpu9VXfWktKH5uEJiZdNyD9TY+xZ2Ekwc6trDjTSFPbxVNaITJGqMBFsuWXGcHvaqoo6bC7Q9r/pVsUHq5KDdoi0zuW+xBilMxk/hZE8fBifXkUZ+KGGibyHlseh/uH9U32UHgvyVSsiUjI1j44WNulRnvfN7Mi5HozJTiYbX2iGrL5QQLKkQIWQPWV37VgQ==",
    "componentDelta": "OEIyAAUL1Py3/oKewtNXswtkYOw+krJP0EFhucFWFXSug0TCV7kqL67Mk5PTzVqNWTAyPl0lK6ac2EBK3kxskC6WpzpJI4qSv7/9JSfQ7zAYUiKAKPobIXpHAJ7BuHSMlMkv/6UTJvdIRsgDaqfAbD5pqG5KDbRzXpzmLIpVJnGyPCkwwm+F36wGbe1ccuvzDHNL77e6XSmm2LpzO/NAGJRjMGXdLQ9XKFvjr/gK0ruO2gdqglomlvy3MG8BSvLCAYkOL1CAB4wF8ovsfpOAAV92KRdqxeMISntCc0/Fxg7fs9JILmn4ZkgiSgha1CsN"
}
```
Response Body may contain either componentDelta or componentFallBack elements.
<ol>
    <li>componentDelta: is encrypted ConnectPayAPI response</li>
    <li>componentFallBack : is unencrypted response and is only triggered in cases of ,Sessiontimeout(responsefromApigee) and Encryption decryptionlogicfailsonConnectPayAPI(inthiscaseencryption/decryption failed so not able to give back encrypted response).</li>
</ol>

### Make The Request
Using the correct endpoint, headers, and encrypted payload, we can then make the call. The ConnectPay backend will decrypt the payload and process the request. It will then return the response encrypted with the AES key and IV provided by componentX and componentY. An example of the output is shown below:
```json
{
"componentDelta": "cRD5xVaJab13iRQ7l6No6ot9YPTFT3bi/qapHYGgsNmxQ8nT2mtIz7uLLHz5kdp5JEmDjiP1dXMNPg8jP5rIZQf/5dtMfFLq7YL7FQY/boTsd7BoJg7reDeeAk6l9+76gaSAZMIRJGYS4fhy1bgClx2jIeWo4fLlfildeHnghCU1ElR8XhFi3oyd8hU+YEpDENP5IJJMVxjnYChuFX8paVy/SAYFMESBXSTIgPi6Y/kJc/bswlxaa9Yei4GnD+Ny1laVs4HqJp32JJ+NHJIYdZr5117AY0JJxJ9oudnkK6J8oPnnXhLCBGxNCRDJG3AVLRxDnQcds/cSiwAVREHr4nn848IEsUb27wJR7SiDxVaELxme9CNZ1dB0tPYQ1wux3ymWtnUgLfVRFsHH3EeucbHv8uIc8dxcwxZReROzVS8="
}
```