# Bank Login Enrollment Architecture
## Explanation of Feature
This is the preferred method of consumer enrollment into ConnectPay.For uCom merchants, skip the details in this section and refer to Sec#3.8.1
<p>
The consumer is presented with an option to login into his/her bank account using their bank username and password. Once the consumer logs in, authorizes the bank account he/she wants to use for this enrollment, and submits, ConnectPay fetches the consumer demographic and/or bank information from the bank using a secure backend connection and populates all the details on the consumers enrollment screen. The consumer will then verify all the details and edit them as he/she sees fit (except for bank account details) and submits the enrollment.
</p>
<p>
This method of enrollment is preferred because it is easier for a consumer to remember the bank username and password as opposed to routing and account number to be keyed in (manual enrollment process). Additionally this method of enrollment is, in most cases, instantly activated and the consumer is ready to transact once their enrollment is successful.
Sequence of activities for completing bank login enrollment:
</p>
## Implementation Steps: Bank Login Process

### Create Consumer Profile (If fdCustomerId not already present for the user) 
[Create Consumer Profile](https://qa-developer.fiserv.com/product/ConnectPay/docs/?path=./documentation/implementationguide.md&branch=develop 'Create Consumer Profile')
### Create Session Token 
[Create Session Token](https://qa-developer.fiserv.com/product/ConnectPay/api/?type=post&path=/security/createsessiontoken&branch=develop&version=1.0.0 'Create Session Token')
### Initialize and Launch ConnectPay SDK <LINK>
You will want to go to the specific mobile operating section and look to initialize the App
[WebSDK](https://qa-developer.fiserv.com/product/ConnectPay/docs/?path=documentation/websdk.md&branch=develop 'Web SDK Instructions')
[iOS]([(https://qa-developer.fiserv.com/product/ConnectPay/docs/?path=documentation/iossdk.md&branch=develop)'iOS SDK Instructions')
[Android]((https://qa-developer.fiserv.com/product/ConnectPay/docs/?path=documentation/androidsdk.md&branch=develop)'Android SDK Instructions')

#### Pass necessary data to the SDK 
After Initialization, Continue to follow the steps to pass through the SDK. Continue to follow the necessary data depending on your SDK. 

<p>Following are the steps to take to complete bank login</p>
<ol>
  <li>SDK presents the screens to the consumer to login into the bank </li>
  <li>Consumer logs in and authorizes a bank account and submits</li>
  <li>ConnectPay encrypts retrieved information and sends encrypted data back to SDK</li>
  <li>SDK decrypts the data and populates the details on the consumer enrollment screen</li>
  <li>Consumer verifies and edits information (except bank number) and submits data for enrollment</li>
  <li>SDK completes enrollment process and returns NONCE to merchantApp</li>
  <li>NONCE passed back to merchant server</li>
  <li>Merchant server does a server-to-server GetData call to retrieve fdAccountId generated after consumer data vaulting. Merchant receives the current consumer status as a part of this call</li>
  <li>Merchant server stores the fdCustomerId,fdAccountId(optional) against the externalId in their system for future use</li>
</ol>

### Issues with Integration
[Fiserv Implementation Support Team](mailto:DL-GBL-VASDelivery@fiserv.com?subject=Issue with Implementation: Bank Login Enrollment Issue)
<p>Image on the flow of the activity</p>
<center><img src="https://raw.githubusercontent.com/Fiserv/connect-pay/develop/assets/images/Online Bank Login Enrollment Architecture.png" alt="Bank Login Architecture" class="center"></center>

