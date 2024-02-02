# ACH Transaction Architecture
Depending on merchant setup, ACH Transactions can be sent to ConnectPay using:
## Universal Commerce (Connected Commerce)
<INSERT LINK>

ConnectPayPayment through FirstAPI
This section will cover ConnectPayPayment through FirstAPI.
For #1 and #2, please refer to the respective implementation guides from uCom <LINK>and Buypass <LINK>.
All payments are server-to-server communication between the merchant server and FirstAPI. Transactions can be initiated using fdAccountId or, connectPayPaymentNumber.
Sequence of activities for completing ACH Transaction scenario:
A. Create Session Token <LINK>
B. Merchant server to encrypt ACH Transaction payload using encryption mechanism specified.
C. Merchant server makes server to server call to ConnectPay at FirstAPI and sends encrypted ACH
Transaction Payload
D. ConnectPay at FirstAPI responds back with encrypted response payload
E. Merchant server decrypts response payload and takes action accordingly

### Flow for uCom merchants
3.8.1 Bank Login Enrollment Architecture
This is the preferred method of consumer enrollment into ConnectPay.
The consumer is presented with an option to login into his/her bank account using their bank username and password. Once the consumer logs in, authorizes the bank account he/she wants to use for this enrollment, and submits, ConnectPay fetches the consumer demographic and/or bank information from the bank using a secure backend connection and populates all the details on the consumers enrollment screen. The consumer will then verify all the details and edit them as he/she sees fit (except for bank account details) and submits the enrollment.
Sequence of activities for completing bank login enrollment for uCom merchants:
A. CreateSessionToken
B. InitializeandLaunchConnectPaySDK
C. PassnecessarydatatotheSDK(includinguComprovidedfdCustomerId)
D. SDKpresentsthescreenstotheconsumertologinintothebank
E. Consumerlogsinandauthorizesabankaccountandsubmits
F. ConnectPay fetches consumer demographic and bank information using a secure backend connection
G. ConnectPay encrypts retrieved information and sends encrypted data back to SDK
H. SDKdecryptsthedataandpopulatesthedetailsontheconsumerenrollmentscreen
I. Consumer verifies and edits information (except bank number) and submits data for enrollment
J. SDK completes enrollment process and returns NONCE to merchant App
K. NONCEpassedbacktomerchantserver
L. Merchant server does a server-to-server GetData call to retrieve fdAccountId generated after consumer data vaulting. Merchant receives the current consumer status as a part of this call.

Merchant server stores the fdCustomerId, fdAccountId (optional) against the externalId in their system for future use.
## Buypass
<INSERT LINK>

<center><img src="https://raw.githubusercontent.com/Fiserv/connect-pay/develop/assets/images/ACH Transaction Arch.png" alt="Non Enrollment Architecture" class="center"></center>