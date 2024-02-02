# ConnectPay Payment Number update
ConnectPayPaymentNumber update generates a new fdAccountId, which is different than other updates to consumer information and needs to be called out. At the end of the ConnectPayPaymentNumber update, the merchant needs to update their record with the new fdAccountId for the payment instrument.
For uCom merchants, skip the details in this section and refer to Sec#3.8.5

Sequence of activities for completing ConnectPayPaymentNumber update:
A. CreateSessionToken(passinginfdAccountIdforconsumer)
B. InitializeandLaunchConnectPaySDK
C. PassnecessarydatatotheSDK(includingfdCustomerId)
D. SDKpresentsthescreenstoconsumertocaptureconsumerinformation
E. SDKcompletesupdateprocessandreturnsNONCEtomerchantApp
F. NONCE passed back to merchant server
G. Merchant server does a server to server GetData call to retrieve fdAccountId generated after consumer data update.
H. Merchantserverstores/updatesthenewfdAccountIdagainsttheexternalId,forthepayment instrument in question, in their system for future use.


![Non Enrollment Architecture](https://raw.githubusercontent.com/Fiserv/connect-pay/develop/assets/images/Payment Number Architecture.png)
