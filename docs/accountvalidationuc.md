# Account Validation Architecture
## Explanation of Feature
This use case should be used in the scenario where the consumer enrollment is already present on the ConnectPay backend, and the consumer wishes to load the existing enrollment into his/her mobile app.
For uCom merchants, skip the details in this section and refer to

The consumer will be provided with a screen to provide their ConnectPayPaymentNumber and PIN for an existing enrollment. Once the consumer submits this page, ConnectPay validates the ConnectPayPaymentNumber and PIN combination. If the validation is successful, the consumer data is updated in vault for mobile processing and a `fdAccountId` is generated for this ConnectPayPaymentNumber.
Sequence of activities for completing Account Validation scenario:

## Implementation Steps: Bank Login Process
### Create Session Token 
<p>
[Create Session Token](https://qa-developer.fiserv.com/product/ConnectPay/api/?type=post&path=/security/createsessiontoken&branch=develop&version=1.0.0)
</p>

### Initialize and Launch ConnectPay SDK 
You will want to go to the specific mobile operating section and look to initialize the App
<p>
[WebSDK](https://qa-developer.fiserv.com/product/ConnectPay/docs/?path=documentation/websdk.md&branch=develop)
</p>
<p>
[iOS](https://qa-developer.fiserv.com/product/ConnectPay/docs/?path=documentation/iossdk.md&branch=develop)
</p>
<p>
[Android]((https://qa-developer.fiserv.com/product/ConnectPay/docs/?path=documentation/androidsdk.md&branch=develop)
</p>

### Additional Steps
<ol>
  <li>Pass necessary data to the SDK (including `fdCustomerId`)</li>
  <li>SDK presents the screens to consumer to capture consumer information</li>
  <li>SDK completes update process and returns NONCE to merchantApp</li>
  <li>NONCE passed back to merchant server</li>
  <li>Merchant server does a server to server GetData call to retrieve fdAccountId generated after consumer data update </li>
  <li>Merchant server stores/updates the `fdAccountId` against the `externalId`,for the payment instrument in question, in their system for future use </li>
</ol>
<!-- theme: danger 
If Account Validation call is invoked multiple times for the same consumer and payment number, the consumer will receive a successful response with the same `fdAccountId` for the ConnectPay payment number, every time.
-->
<p>Image on the flow of the activity</p>

### Issues with Integration
[Fiserv Implementation Support Team](mailto:DL-GBL-VASDelivery@fiserv.com)
<center><img src="https://raw.githubusercontent.com/Fiserv/connect-pay/develop/assets/images/Account Validation Architecture.png" alt="Non Enrollment Architecture" class="center"></center>
