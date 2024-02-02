# Manual Enrollment Architecture
The consumer has an option to manually key in all information required for ConnectPay enrollment into the enrollment screen.
Usually after a manual enrollment, two micro deposits are made to the consumer’s bank account. The consumer waits for 1-3 business days for these micro deposits to appear in their bank account, following which he/she needs to validate their account by answering micro deposit amount questions via the Micro Deposit Validation process.
The consumer is in a pending validation status and will not be able to transact until the validation is completed.
Sequence of activities for completing manual enrollment for uCom merchants:
A. CreateSessionToken 
B. InitializeandLaunchConnectPaySDK
C. PassnecessarydatatotheSDK(includinguComprovidedfdCustomerId)
D. SDKpresentsthescreenstoconsumertocaptureconsumerinformation
E. SDKcompletesenrollmentprocessandreturnsNONCEtomerchantApp
F. NONCE passed back to merchant server
G. Merchant server does a server-to-server GetData call to retrieve fdAccountId generated after consumer data vaulting. Merchant additionally receives the current consumer status as a part of this call.
Merchant server stores the fdCustomerId, fdAccountId (optional) against the externalId in their system for future use.

<center><img src="https://raw.githubusercontent.com/Fiserv/connect-pay/develop/assets/images/Manual Enrollment Arch.png" alt="Manual Enrollment Architecture" class="center"></center>
