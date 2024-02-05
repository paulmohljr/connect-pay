# ACH Transaction Architecture
Depending on merchant setup, ACH Transactions can be sent to ConnectPay using:
<ol>
<li>[uCOM]((https://qa-developer.fiserv.com/product/)'uCom Merchant')</li>
<li>[Buypass]((https://qa-developer.fiserv.com/product/)'Buypass Merchant')</li>
<li>ConnecPayPayment through FirstAPI (Continue Below)</li>
</ol>
*Note: For uCOM and Buypass, you will need to refer to the respective Implementation guide links above for setup*

## Explanation of Feature
All payments are server-to-server communication between the merchant server and FirstAPI. Transactions can be initiated using fdAccountId or, connectPayPaymentNumber

## Implementation Steps: ACH Transaction Process
### Create Session Token 
[Create Session Token](https://qa-developer.fiserv.com/product/ConnectPay/api/?type=post&path=/security/createsessiontoken&branch=develop&version=1.0.0 'Create Session Token')
### Additional Steps
<ol>
  <li>Merchant server makes server to server call to ConnectPay at FirstAPI and sends encrypted ACH
Transaction Payload</li>
  <li>ConnectPay at FirstAPI responds back with encrypted response payload</li>
  <li>Merchant server decrypts response payload and takes action accordingly</li>

### Issues with Integration
[Fiserv Implementation Support Team](mailto:DL-GBL-VASDelivery@fiserv.com?subject=Issue with Implementation: ACH Transation Issue)
<p>Image on the flow of the activity</p>
<center><img src="https://raw.githubusercontent.com/Fiserv/connect-pay/develop/assets/images/ACH Transaction Arch.png" alt="ACH Transaction Architecture" class="center"></center>