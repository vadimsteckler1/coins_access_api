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
   * - soiJobTitle
     - string
     - yes
     - Job     
