# Non-enrollment Architecture
## Explanation of Feature
This section would cover business use cases like MicroDepositValidation, ConsumerUpdates (other than ConnectPayPaymentNumber updates) and ACH account closure.
For uCom merchants, skip the details in this section and refer to Sec
Sequence of activities for completing Non Enrollment scenario:

### Create Session Token 
[Create Session Token](https://qa-developer.fiserv.com/product/ConnectPay/api/?type=post&path=/security/createsessiontoken&branch=develop&version=1.0.0 'Create Session Token')
### Initialize and Launch ConnectPay SDK <LINK>
You will want to go to the specific mobile operating section and look to initialize the App
[WebSDK](https://qa-developer.fiserv.com/product/ConnectPay/docs/?path=documentation/websdk.md&branch=develop 'Web SDK Instructions')
[iOS]([(https://qa-developer.fiserv.com/product/ConnectPay/docs/?path=documentation/iossdk.md&branch=develop)'iOS SDK Instructions')
[Android]((https://qa-developer.fiserv.com/product/ConnectPay/docs/?path=documentation/androidsdk.md&branch=develop)'Android SDK Instructions')

### Further Steps
<ol>
  <li>Pass necessary data to the SDK(including fdCustomerId)</li>
  <li>SDK presents the screens to consumer to capture consumer information</li>
  <li>SDK completes update process and displays response to consumer</li>
</ol>
### Issues with Integration
[Fiserv Implementation Support Team](mailto:DL-GBL-VASDelivery@fiserv.com?subject=Issue with Implementation: Non-Enrollment Issues)
<p>Image on the flow of the activity</p>
<center><img src="https://raw.githubusercontent.com/Fiserv/connect-pay/develop/assets/images/Non-Enrollment Architecture.png" alt="Non Enrollment Architecture" class="center"></center>