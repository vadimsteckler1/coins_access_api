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
     - String
     - yes
     - Country code of the region where the user is based, e.g. PH
   * - kycLevel
     - String
     - yes
     - KYC level, e.g. lv0,lv1,lv2,lv3
   * - firstName
     - String
     - yes
     - User’s first name
   * - middleName
     - String
     - no
     - User’s middle name
   * - last name
     - String
     - yes
     - User’s last name
   * - dateOfBirth
     - String
     - yes
     - User’s date of birth. The date format patterns to use: 'yyyy-MM-dd HH:mm:ss'
