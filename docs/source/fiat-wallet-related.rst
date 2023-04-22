Fiat and E-Wallet Related Endpoints
======================

PHP Cash-In
-----------
As shown in the diagram below, the PHP cash-in process includes the following steps:

.. image::
   PHP_dom_cashin.png
   
InstaPay/PESONet Cash-In
~~~~~~~~~~~~~~~~~~~~~~~~
This module is used for the e-wallet/bank (InstaPay/PESONet) implementation of cash-in operations.

Retrieving User Cash-In Account Information
~~~~~~~~~~~~~~~~~~~~~~~~

**Method:** GET

**URL:** /merchant-api/fiat/cash-in/info?userId=13530199609

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

E-wallet Transfer steps
~~~~~~~

1. Select send money to a bank account on your wallet app.
2. Choose InstaPay/PESONet as transfer option.
3. Enter the account details and enter the amount you want to cash in.

   - Bank: DCPay Philippines/Coins.ph

   - Account Name: Your full name 

   - Account Number:  Your union ID number (provided by Coins to route cash-ins to the appropriate merchant and end user account; e.g., “0200000002”)
4. The amount will be credited to your PHP balance once the transaction has been processed.

Online bank Transfer steps
~~~~~~~
1.Choose to transfer funds to another bank account.
2.Choose InstaPay/PESONet as transfer option.
3.Enter the account details below and enter the amount you want to cash in.

   - Bank: DCPay Philippines/Coins.ph
   
   - Account Name: Your full name
   
   - Account Number: Your union ID number (provided by Coins to route cash-ins to the appropriate merchant and end user account; e.g. “0200000002”)
4. The amount will be credited to your PHP balance once the transaction has been processed.

Special Instructions
~~~~~~~
1. Supports E-wallet/banks see transaction/fiat/query-supported-channels endpoint
2. Each merchant has a consistent and different merchant prefix code, and union ID number designated to their end user account in order to route an incoming InstaPay or PESONet transfer to the correct merchant’s end user account.

Passive cash-in process description
~~~~~~~
InstaPay/PESONet cash-in operations need to be initiated from a third-party bank or e-wallet. The specific process is delineated below (Coins.ph e-wallet UI appears only as an example):

.. image::
   PHP_dom_cashin.png

.. image::
   PHP_dom_cashin.png

