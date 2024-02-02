# Account Validation Architecture

This use case should be used in the scenario where the consumer enrollment is already present on the ConnectPay backend, and the consumer wishes to load the existing enrollment into his/her mobile app.
For uCom merchants, skip the details in this section and refer to Sec#3.8.3
The consumer will be provided with a screen to provide their ConnectPayPaymentNumber and PIN for an existing enrollment. Once the consumer submits this page, ConnectPay validates the ConnectPayPaymentNumber and PIN combination. If the validation is successful, the consumer data is updated in vault for mobile processing and a fdAccountId is generated for this ConnectPayPaymentNumber.
Sequence of activities for completing Account Validation scenario:
A. CreateSessionToken
B. InitializeandLaunchConnectPaySDK
C. PassnecessarydatatotheSDK(includingfdCustomerId)
D. SDKpresentsthescreenstoconsumertocaptureconsumerinformation
E. SDKcompletesupdateprocessandreturnsNONCEtomerchantApp
F. NONCE passed back to merchant server
G. Merchant server does a server to server GetData call to retrieve fdAccountId generated after consumer data update.
H. Merchantserverstores/updatesthefdAccountIdagainsttheexternalId,forthepayment instrument in question, in their system for future use.
Note: If Account Validation call is invoked multiple times for the same consumer and payment number, the consumer will receive a successful response with the same fdAccountId for the ConnectPay payment number, every time.

![Non Enrollment Architecture](https://raw.githubusercontent.com/Fiserv/connect-pay/develop/assets/images/Account Validation Architecture.png)