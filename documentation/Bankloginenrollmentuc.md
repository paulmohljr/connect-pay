# Bank Login Enrollment Architecture
This is the preferred method of consumer enrollment into ConnectPay.
For uCom merchants, skip the details in this section and refer to Sec#3.8.1
The consumer is presented with an option to login into his/her bank account using their bank username and password. Once the consumer logs in, authorizes the bank account he/she wants to use for this enrollment, and submits, ConnectPay fetches the consumer demographic and/or bank information from the bank using a secure backend connection and populates all the details on the consumers enrollment screen. The consumer will then verify all the details and edit them as he/she sees fit (except for bank account details) and submits the enrollment.

This method of enrollment is preferred because it is easier for a consumer to remember the bank username and password as opposed to routing and account number to be keyed in (manual enrollment process). Additionally this method of enrollment is, in most cases, instantly activated and the consumer is ready to transact once their enrollment is successful.
Sequence of activities for completing bank login enrollment:

A. CreateConsumerProfile(IffdCustomerIdnotalreadypresentfortheuser)  - <LINK>
B. CreateSessionToken <LINK>
C. InitializeandLaunchConnectPaySDK <LINK>
D. PassnecessarydatatotheSDK <LINK>
E. SDKpresentsthescreenstotheconsumertologinintothebank <LINK>
F. Consumer logs in and authorizes a bank account and submits

G. ConnectPay fetches consumer demographic and bank information using a secure backend connection
H. ConnectPayencryptsretrievedinformationandsendsencrypteddatabacktoSDK <LINK>
I. SDK decrypts the data and populates the details on the consumer enrollment screen
J. Consumer verifies and edits information (except bank number) and submits data for enrollment
K. SDKcompletesenrollmentprocessandreturnsNONCEtomerchantApp <LINK>
L. NONCE passed back to merchant server
M. Merchant server does a server-to-server GetData call to retrieve fdAccountId generated after consumer data vaulting. Merchant receives the current consumer status as a part of this call.
N. MerchantserverstoresthefdCustomerId,fdAccountId(optional)againsttheexternalIdin their system for future use.

<center><img src="https://raw.githubusercontent.com/Fiserv/connect-pay/develop/assets/images/Online Bank Login Enrollment Architecture.png" alt="Bank Login Architecture" class="center"></center>
