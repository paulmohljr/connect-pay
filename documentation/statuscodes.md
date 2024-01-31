# Error Codes 
 Listed Below are common codes being returned in Connect Pay. 

|Service| HTTP Status Code | Transaction Status Code | Transaction Status Description | Transaction Error Code | Transaction Error Description | Field Name|
|---------|-------------|-------------------------|--------------------------------|-----|--------------------------------------------------|------------|
|Enrollment|200|70|Validations Pending||||
|Enrollment|200|90|Prior Pending||||
|Enrollment|201|0|Created ||||
|Enrollment|201|70|Validations Pending||||
|Enrollment|400|100|Input is invalid|1010|Field did not have a valid format|fdCustomerID,type,OnlineBankTransactionId,State,Country,Postal Code,Email,MobilePhone,Primary Phone,RoutingNumber,Account Number,DriverLicenseNumber,DriverLicenseState,Dob,SocialSecurityNumber,SecurityQuestionId,SecurityQuestion,SecurityAnswer, ConnectPayPaymentNumber,Gender,MemberSince,TermsAndConditionsVersion,Pin,ReportingFieldOne,ReportingFieldTwo,ReportingFieldThree,GenericFlagOne,GenericFlagTwo,GenericFlagThree, GenericCodeOne,GenericCodeTwo,GenericCodeThree,Application,ApplicationId,Device,DeviceId,I PAddress,IMEI,SubscriberId,OrganizationId,SessionId,TrueIPAddress,ConsumerId,FirstName,Last Name,Street,Street2,City,Corporate Check|
|Enrollment|400|100|Input is invalid|1020|fdCustomerID,type,DLN,DLState, MemberSince,DriverLicenseNumber,DriverLicenseState,SocialSecurityNumber,State,Phone1-Type,Phone1-Number,Phone1-Extension,Phone1-Primary,Phone2-Type,Phone2-Number,Phone2-Extension,Phone2-Primary,Phone3-Type,Phone3-Number,Phone3-Extension,Phone3-Primary,Phone4-Type,Phone4-Number,Phone4-Extension,Phone4-Primary,RoutingNumber,Account Number,RoutingNumber/AccountNumber,OnlineBankTransactionId,Dob|
|Enrollment|400|100|Input is invalid|1030|Required field did not have a value|fdCustomerID,type,securityQuest ionId,securityQuestion,securityAnswer,BankDetails,Phone1-Type,Phone1-Number,Phone1-Primary,Phone2-Type,Phone2-Number Phone2-Primary,Phone3-Type,Phone3-Number,Phone3-Primary,Phone4-Type,Phone4- Number,Phone4-Primary,DriverLicenseNumber,DriverLicenseState,AccountNumber,RoutingNumber,FirstName,Last Name,Street,Dob,City,State,Country,PostalCode,Email,MemberSince,Pin,ConnectPayPaymentNumber|
|Enrollment|400|100|Input is invalid|1035|Required field is missing
|Enrollment|400|100|Input is invalid|1040|Required block did not have a value
|Enrollment|400|100|Input is invalid|1045|Required block is missing
|Enrollment|400|100|Input is invalid|1050|Fields contain values more than that is allowed
|Enrollment|400|100|Input is invalid|1060|Required header field is missing
|Enrollment|400|100|Input is invalid|1080|Block contain values more than that is allowed
|Enrollment|400|100|Input is invalid|1380|Phone block should has only one primary phone| Phone-Primary|
|Enrollment|400|100|Input is invalid|1390|Either Bank Details or MICR Details or PWMBTransactionId must have values| OnlineBankTransactionId
|Enrollment|400|100|Input is invalid|1400|ConnectPayPaymentNumber is Invalid|ConnectPayPaymentNumber|
|Enrollment|400|100|Input is invalid|1430|ConnectPayPaymentNumber|
|Enrollment|400|120|Consumer Cannot Be Validated|2030|Entity is not in a valid state for action|ConnectPayPaymentNumber|
|Enrollment|400|120|
|Enrollment|400|130|
|Enrollment|400|140|
|Enrollment|400|140|
|Enrollment|400|400|
|Enrollment|400|400|