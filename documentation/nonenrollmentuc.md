# Non-enrollment Architecture

This section would cover business use cases like MicroDepositValidation, ConsumerUpdates (other than ConnectPayPaymentNumber updates) and ACH account closure.
For uCom merchants, skip the details in this section and refer to Sec
Sequence of activities for completing Non Enrollment scenario:
A. CreateSessionToken(passinginfdAccountIdforconsumer)
B. InitializeandLaunchConnectPaySDK
C. PassnecessarydatatotheSDK(includingfdCustomerId)
D. SDKpresentsthescreenstoconsumertocaptureconsumerinformation E. SDKcompletesupdateprocessanddisplaysresponsetoconsumer.


![Non Enrollment Architecture](https://raw.githubusercontent.com/Fiserv/connect-pay/develop/assets/images/Non-Enrollment Architecture.png)