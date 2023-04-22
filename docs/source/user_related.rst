User Related Endpoints
======================
The diagram below delineates the user registration and KYC review process:

.. image::
   User_Related_Endpoints.png
Sharing User’s KYC Information with Coins Access and Registering the User
---------------------------------------------------------------------

When opening an account with the Merchant, the user submits the required KYC information. This endpoint is used to share the user’s KYC information with Coins Access and register them at Coins Access.

**Method:** POST

**URL:** /merchant-api/account/kyc-share-and-register

**Idempotent:** True

Request
~~~~~~~

.. list-table::
   :header-rows: 1

   * - Parameter Name
     - Layout
     - Required
     - Description
   * - userId
     - Request Body
     - yes
     - User ID in the Merchant’s platform 
   * - email
     - Request Body
     - no
     - Email address
   * - phone
     - Request Body
     - yes
     - Mobile number. At least one email or phone must be provided.
   * - verified
     - Request Body
     - no
     - Indicates whether the user was verified by Merchant
   * - verifiedTime
     - Request Body
     - no
     - If the user was verified by Merchant, this parameter indicates the verification time
   * - needRecheck
     - Request Body
     - no
     - Indicates whether Coins must recheck the user’s KYC 
   * - kycType
     - Request Body
     - yes
     - User kyc type (e.g. kyc, kyb)
   * - kycInfo
     - Request Body
     - yes
     - The user’s information that Merchant shares with Coins. See an example below.

KYC information 
~~~~~~~

.. list-table::
   :header-rows: 1
   
   * - Field name
     - Data type
     - Required
     - Description
   * - residence
     - string
     - yes
     - Country code of the region where the user is based, e.g. PH
   * - kycLevel
     - string
     - yes
     - KYC level, e.g. lv0,lv1,lv2,lv3
   * - firstName
     - string
     - yes
     - User’s first name
   * - middleName
     - string
     - no
     - User’s middle name
   * - last name
     - string
     - yes
     - User’s last name
   * - dateOfBirth
     - string
     - yes
     - User’s date of birth. Use the following date format pattern: 'yyyy-MM-dd HH:mm:ss'
   * - countryOfBirth
     - string
     - yes
     - User’s country of birth
   * - Gender
     - integer
     - yes
     - User’s gender. For example, 1: Male 2: Female
   * - nationality
     - string
     - yes
     - User’s nationality
   * - currentCountry
     - string
     - yes
     - Current country of residence
   * - currentState
     - string
     - yes
     - Current state of residence
   * - currentCity
     - string
     - yes
     - Current city of residence
   * - currentStreet
     - string
     - yes
     - The street where the user currently resides
   * - currentZipCode
     - string
     - yes
     - ZIP code of the area where the user currently resides     
   * - permCountry
     - string
     - no
     - Country of permanent residence
   * - permState
     - string
     - no
     - State of permanent residence
   * - permCity
     - string
     - no
     - City of permanent residence
   * - permStreet
     - string
     - no   
     - The street where the user permanently resides
   * - permZipCode
     - string
     - no
     - ZIP code of the area where the user permanently resides
   * - poaDocType
     - string
     - no
     - Detailed information about Proof of Address:
       
       - 'credit_card_bill' : Credit Card Bill
       
       - 'utility_bill' : Utility Bill (water, electricity, cable, phone)
       
       - 'phone_bill' : Mobile Phone Bill
       
       - 'umid' : UMID
       
       - 'tax_return' : Income tax return (Form 2316)
       
       - 'cert_barangay' : Barangay Clearance/ Barangay Certification of Residency
       
       - 'certificate' : Certificate from University, Government Institution, or Embassy
       
       - 'insurance' : Statement of Account - Life Insurance
   * - poaDocs
     - array
     - no
     - Proof of Address document, which is encoded in base64 (if any), such as: "/9j/4AA..[omitted]..PxA="
   * - soiEmploymentStatus
     - string
     - yes
     - Detailed information about the Source of Income(SOI):
     
       - 'employed' : Employed
       
       - 'self_e' : Self Employed
       
       - 'freelance' : Freelancer
       
       - 'unemployed' : Unemployed
       
       - 'retired' : Retired
       
       - 'student' : Student
   * - soiIndustry
     - string
     - yes
     - Industry or sector in which the source of income of the individual belongs to
   * - soiCompanyName
     - string
     - yes
     - Name of the company where the individual is employed
   * - soiJobTitle
     - string
     - yes
     - Job title or position of the individual in their current employment     
   * - soiSourceOfFunds
     - string
     - yes
     - Origin of the funds that will be used for the account
   * - soiProofType
     - string
     - no
     - Type of proof document submitted as a source of identification or verification:
     
       - 'payslip' : Payslip
       
       - 'cert_employment' : Certificate of Employment
       
       - 'tax_return' : Your Latest Income Tax Return
       
       - 'contract' : valid contract
   * - soiProofDoc
     - string
     - no
     - Proof document uploaded by the individual to verify their source of income.
   * - idType
     - string
     - yes
     - Detailed information about document verification. The following document types are supported:
     
       - 'passport' : International Passport
       
       - 'passport-old' : Philippines Passport - old version
       
       - 'passport-new' : Philippines Passport - new version
       
       - 'umid' : Unified Multi-Purpose ID
       
       - 'driver' : Driver’s license
       
       - 'sss' : Social Security System ID
       
       - 'postal' : Postal ID
       
       - 'prc' : PRC ID
       
       - 'voter' : Voter's ID
       
       - 'philhealth' : PhilHealth ID
       
       - 'philsys' : Philsys National ID
   * - idNumber
     - string
     - yes
     - Unique identification number assigned to the individual by a governmental or authorized agency     
   * - idFirstName
     - string
     - no
     - First name of the individual as it appears on their identification document
   * - idMiddleName
     - string
     - no
     - Middle name of the individual as it appears on their identification document
   * - idLastName
     - string
     - no
     - Last name of the individual as it appears on their identification document
   * - idGender
     - integer
     - no
     - Gender of the individual as it appears on their identification document. For example, 1: Male 2: Female
   * - idDob
     - string
     - no
     - Date of birth of the individual as it appears on their identification document. Use the following date format pattern: 'yyyy-MM-dd HH:mm:ss'
   * - idAddress
     - string
     - no
     - Address of the individual as it appears on their identification document
   * - idExpirationDate
     - string
     - no
     - Expiration date of the identification document
   * - idIssuanceCountry
     - string
     - no
     - Country where the identification document was issued
   * - idIssuanceDate
     - string
     - no
     - Date on which the identification document was issued
   * - idNationality
     - string
     - no
     - Nationality of the individual as it appears on their identification document
   * - idRegistrationDate
     - string
     - no
     - Date of registration for the identification document     
   * - frontImg
     - string
     - yes
     - The front side image of the identity document, encoded in base64 and provided as a string of characters, such as ``/9j/4AA..[omitted]..PxA=``.
   * - backImg
     - string
     - no
     - The back side image of the identity document (if any), encoded in base64 and provided as a string of characters, such as ``/9j/4AA..[omitted]..PxA=``.
   * - liveCheckImg
     - string
     - no
     - Image of the user's face taken during the KYC process, encoded in base64 and provided as a string of characters, such as ``/9j/4AA..[omitted]..PxA=``.
   * - selfieImg
     - string
     - yes
     - The user's selfie encoded in base64 and provided as a string of characters, such as ``/9j/4AA..[omitted]..PxA=``.

Sample KYC Information
~~~~~~~

.. code-block:: JSON

   {
       "userId":"12af3vf3",
       "email":"abc@gmail.com",
       "phone":"+639171234567",
       "verified": true,
       "verifiedTime":"2022-03-11T14:00:22",
       "kycType":"kyc",
       "kycInfo":{
           "residence":"PH",
           "kycLevel":"2",
           "firstName":"string",
           "middleName":"string",
           "lastName":"string",
           "dateOfBirth":"1990-01-23 00:00:00",
           "countryOfBirth":"string",
           "gender":"string",
           "nationality":"string",
           "currentCountry":"string",
           "currentState":"string",
           "currentCity":"string",
           "currentStreet":"string",
           "currentZipCode":"string",
           "permCountry":"string",
           "permState":"string",
           "permCity":"string",
           "permStreet":"string",
           "permZipCode":"string",
           "poaDocType":"string",
           "poaDocs":[
               "/9j/4AA..[omitted]..PxA=",
               "/9j/4AA..[omitted]..PxA="
           ],
           "soiEmploymentStatus":"string",
           "soiIndustry":"string",
           "soiCompanyName":"string",
           "soiJobTitle":"string",
           "soiSourceOfFunds":"string",
           "soiProofType":"string",
           "soiProofDoc":"/9j/4AA..[omitted]..PxA=",
           "idType":"string",
           "idNumber":"string",
           "idFirstName":"string",
           "idMiddleName":"string",
           "idLastName":"string",
           "idGender":"string",
           "idDob":"string",
           "idAddress":"string",
           "idExpirationDate":"string",
           "idIssuanceCountry":"string",
           "idIssuanceDate":"string",
           "idNationality":"string",
           "idRegistrationDate":"string",
           "frontImg":"/9j/4AA..[omitted]..PxA=",
           "backImg":"/9j/4AA..[omitted]..PxA=",
           "liveCheckImg":"/9j/4AA..[omitted]..PxA=",
           "selfieImg":"/9j/4AA..[omitted]..PxA="
       }
   }

Important notes:
~~~~~~~

- If a user was verified by the Merchant, and the Merchant does not require that Coins recheck the user information, then this endpoint will return a result directly. If the user was not verified by the Merchant, Coins will enforce a check and notify the Merchant of the final result through a webhook.

- This endpoint is idempotent. Therefore, if the user is already registered the returned result will be identical. 
  ``lv1Info``, ``lv2Info`` and ``lv3Info`` are optional. If only ``lv1Info`` is shared with Coins, Coins will only verify ``lv1``. Consequently, if this user passes verification, she or he will be considered ``kyc lv1``.

- All documents and photos must be encoded with Base64. The file’s URL is not to be encoded.

Responses
~~~~~~~

**KYC check is required**

.. code-block:: JSON

   {    
          "userId" : "1304304339091773722",
          "registerStatus" : "Processing",
          "kycStatus" : "Processing"

   }


**KYC check is not required**

.. code-block:: JSON

   {    
          "userId" : "1304304339091773722",
          "registerStatus" : "Success",
          "kycStatus" : "Passed"

   }

Retrieving User Status
----------------------
This endpoint fetches the user’s current status.

**Method:** POST

**URL:** /merchant-api/user/query-user-status

**Idempotent:** True

Request
~~~~~~~

.. list-table::
   :header-rows: 1
   
   * - Parameter
     - Layout
     - Required
     - Description
   * - userId
     - Request body
     - yes
     - User ID in the Merchant’s platform

Response
~~~~~~~

.. code-block:: JSON

    "userId" : "1304304339091773722",
    "registerStatus" : "success",
    "kycStatus" : "lv2"

Retrieving User’s KYC Information
----------------------
This endpoint fetches the user’s current KYC information.

**Method:** POST

**URL:** /merchant-api/user/query-user-kyc

**Idempotent:** True

Request
~~~~~~~

.. list-table::
   :header-rows: 1
   
   * - Parameter
     - Layout
     - Required
     - Description
   * - userId
     - Request body
     - yes
     - User ID in the Merchant’s platform
   * - isReturnImage
     - Request body
     - no
     - KYC detail contains images    

Response
~~~~~~~

.. code-block:: JSON

   {
      "kycType":"kyc",
      "kycLevel": "string",
      "firstName": "string",
      "middleName": "string",
      "lastName": "string",
      "dateOfBirth": "string",
      "countryOfBirth": "string",
      "gender": "string",
      "nationality": "string",
      "currentCountry": "string",
      "currentState": "string",
      "currentCity": "string",
      "currentStreet": "string",
      "currentZipCode": "string",
      "purposeOfAccount": "string",
      "idType": "string",
      "idNumber": "string",
      "idAddress": "string",
      "idExpirationDate": "string",
      "idIssuanceCountry": "string",
      "idIssuanceDate": "string",
      "frontImg": "/9j/4AA..[omitted]..PxA=",
      "backImg": "/9j/4AA..[omitted]..PxA=",
      "liveCheckImg": "/9j/4AA..[omitted]..PxA=",
      "selfieImg": "/9j/4AA..[omitted]..PxA="
   }

Updating User Status
----------------------
This endpoint changes the user status to Frozen or Unfrozen.

**Method:** POST

**URL:** /merchant-api/user/update-user-status

**Idempotent:** True

Request
~~~~~~~

.. list-table::
   :header-rows: 1
   
   * - Parameter
     - Layout
     - Required
     - Description
   * - userId
     - Request body
     - yes
     - User ID in the Merchant’s platform
   * - status
     - Request body
     - yes
     - Status: Frozen/Unfrozen     

Response
~~~~~~~

.. code-block:: JSON

   {
       "success":true, // true or false
   }
