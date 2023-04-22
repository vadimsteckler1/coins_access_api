Crypto Wallet Related Endpoints
======================

Fetching User Balance
~~~~~~~~~~~~~~~~~~~~~~~~
This endpoint fetches the current balance in the user wallet.

**Method:** GET

**URL:** /merchant-api/wallet/query-user-balances?userId=abc123&currencies=PHP

**Idempotent:** False

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
   * - currencies
     - Request body
     - no
     - PHP, BTC, ETH
     

Response
~~~~~~~

.. code-block:: JSON

          [
            {
              "PHP" : {
                 "available" : "30000",
                 "locked"  :  "2000",
                 "unconfirmed"  :  "3000",
               }
            }
          ]

P2P Transfer 
~~~~~~~~~~~~~~~~~~~~~~~~
This endpoint performs a wallet-to-wallet transfer between one payer and one payee.

**Method:** POST

**URL:** /merchant-api/wallet/p2p-transfer

**Idempotent:** True

Request
~~~~~~~

.. code-block:: JSON

    {
        "clientTxId":"abc001", //Idempotent，Limit length to 100
        "fromUserId":"10001",
        "toUserId" : "10002",
        "amount" : "0.1",
        "currency" : "BTC"
    }

Response
~~~~~~~

.. code-block:: JSON

  {
      "clientTxId":"abc001",
      "status":"pending", //pending, success, failed
      "remarks": "" 
  }
  //if status=failed, remarks will return enum of failed reason

Remarks Enum
~~~~~~~

.. code-block:: JSON

  FROM_USER_NOT_FOUND
  TO_USER_NOT_FOUND
  INSUFFICIENT_BALANCE
  SYSTEM_ERROR


