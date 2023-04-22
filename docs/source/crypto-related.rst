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

.. code-block:: console

  FROM_USER_NOT_FOUND
  TO_USER_NOT_FOUND
  INSUFFICIENT_BALANCE
  SYSTEM_ERROR

Batch Transfer
~~~~~~~~~~~~~~~~~~~~~~~~
This endpoint performs internal batch transfers between multiple payers and payees; either a single payer to multiple payees, or multiple payers to one payee.

**Method:** POST

**URL:** /merchant-api/wallet/batch-transfer

**Idempotent:** True

Request
~~~~~~~

.. code-block:: JSON

   {  
       "batchTxId":"abc001", //Idempotent
       "details":[{
         "fromUserId":"10001",
         "toUserId" : "10002",
         "amount" : "10",
         "currency" : "PHP"
       },{
         "fromUserId":"10001",
         "toUserId" : "10003",
         "amount" : "20",
         "currency" : "PHP"
       },{
        "fromUserId":"10001",
        "toUserId" : "10004",
         "amount" : "20",
         "currency" : "PHP"
       }]
   }

Response
~~~~~~~

.. code-block:: JSON

   {
       "batchTxId":"abc001",
       "status":"pending", //pending, success, failed
       "remarks": "" 
   }
   //if status=failed, remarks will return enum of failed reason

Remarks Enum
~~~~~~~

.. code-block:: console

   FROM_USER_NOT_FOUND
   TO_USER_NOT_FOUND
   BATCH_TRANSFER_SIZE_TOO_LARGE
   INSUFFICIENT_BALANCE
   SYSTEM_ERROR

Token Information
~~~~~~~~~~~~~~~~~~~~~~~~
Get information of tokens (available for deposits and withdrawals) for the user.

**Method:** GET

**URL:** /merchant-api/wallet/config/getall

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

Response
~~~~~~~

.. code-block:: JSON

   [
       {
           "token": "ETH",
           "name": "ETH",
           "depositAllEnable": true,
           "withdrawAllEnable": true,
           "free": "1.9144",
           "locked": "0.0426",
           "networkList": [
               {
                   "addressRegex": "0x([0-9a-fA-F]){40}",
                   "memoRegex": "^[0-9A-Za-z\\-_]{1,120}$",
                   "network": "ETH",
                   "name": "ERC20",
                   "depositEnable": true,
                   "minConfirm": 8,
                   "unLockConfirm": 12,
                   "withdrawDesc": "1234567890",
                   "withdrawEnable": true,
                   "withdrawFee": "0",
                   "withdrawIntegerMultiple": "0.00000001",
                   "withdrawMax": "1",
                   "withdrawMin": "0.001",
                   "sameAddress": false
               }
           ],
           "legalMoney": false
       }
     ]

Deposit Address
~~~~~~~~~~~~~~~~~~~~~~~~
Fetch deposit address along with token network.

**Method:** GET

**URL:** /merchant-api/wallet/deposit/address

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
   * - token
     - string
     - yes
     - 
   * - network
     - string
     - yes
     -      
Response
~~~~~~~

.. code-block:: JSON

   {
       "token": "ETH",
       "address": "0xfe98628173830bf79c59f04585ce41f7de168784",
       "addressTag": ""
   }

Withdrawal
~~~~~~~~~~~~~~~~~~~~~~~~
Submit a withdrawal request.

**Method:** POST

**URL:** /merchant-api/wallet/withdraw/apply

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
   * - token
     - string
     - yes
     - 
   * - address
     - string
     - yes
     -
   * - addressTag
     - string
     - no
     -
   * - amount
     - decimal
     - yes
     -
   * - withdrawOrderId
     - string
     - no
     -
     
Response
~~~~~~~

.. code-block:: JSON

   {
     "id":"459165282044051456"
   }

Deposit History
~~~~~~~~~~~~~~~~~~~~~~~~
Fetch deposit history.

**Method:** GET

**URL:** /merchant-api/wallet/deposit/history

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
   * - token
     - string
     - no
     - 
   * - txId
     - string
     - no
     -
   * - status
     - integer
     - no
     - 0-PROCESSING, 
       
       1-SUCCESS
       
       2-FAILED
       
       3-NEED_FILL_DATA (travel rule info)
   * - startTime
     - long
     - no
     - Default: 90 days from current timestamp
   * - endTime
     - long
     - no
     - Default: present timestamp
   * - offset
     - integer
     - no
     - Default:0
   * - limit
     - long
     - no
     - Default: 1000, Max: 1000

* Please note the default startTime and endTime to make sure that time interval is within 0-90 days.
* If both startTime and endTime are sent, time between startTime and endTime must be less than 90 days.

Response
~~~~~~~

.. code-block:: JSON

   [
       {
           "id": "d_769800519366885376",
           "amount": "0.001",
           "token": "BNB",
           "network": "BNB",
           "status": 0,
           "address": "bnb136ns6lfw4zs5hg4n85vdthaad7hq5m4gtkgf23",
           "addressTag": "101764890",
           "txId": "98A3EA560C6B3336D348B6C83F0F95ECE4F1F5919E94BD006E5BF3BF264FACFC",
           "insertTime": 1661493146000,
           "confirmNo": 10,
       },
       {
           "id": "d_769754833590042625",
           "amount":"0.5",
           "token":"IOTA",
           "network":"IOTA",
           "status":1,
           "address":"SIZ9VLMHWATXKV99LH99CIGFJFUMLEHGWVZVNNZXRJJVWBPHYWPPBOSDORZ9EQSHCZAMPVAPGFYQAUUV9DROOXJLNW",
           "addressTag":"",
           "txId":"ESBFVQUTPIWQNJSPXFNHNYHSQNTGKRVKPRABQWTAXCDWOAKDKYWPTVG9BGXNVNKTLEJGESAVXIKIZ9999",
           "insertTime":1599620082000,
           "confirmNo": 20,
       }
   ]

Withdrawal History
~~~~~~~~~~~~~~~~~~~~~~~~
Fetch withdrawal history.

**Method:** GET

**URL:** /merchant-api/wallet/withdraw/history

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
   * - token
     - string
     - no
     - 
   * - withdrawOrderId
     - string
     - no
     -
   * - status
     - integer
     - no
     - 0-PROCESSING, 
       
       1-SUCCESS
       
       2-FAILED
       
       3-NEED_FILL_DATA (travel rule info)
   * - startTime
     - long
     - no
     - Default: 90 days from current timestamp
   * - endTime
     - long
     - no
     - Default: present timestamp
   * - offset
     - integer
     - no
     - Default:0
   * - limit
     - long
     - no
     - Default: 1000, Max: 1000

* Please note the default startTime and endTime to make sure that time interval is within 0-90 days.
* If both startTime and endTime are sent, time between startTime and endTime must be less than 90 days.
* If withdrawOrderId is sent, time between startTime and endTime must be less than 7 days.
* If withdrawOrderId is sent, and startTime and endTime are not sent, the last 7 days’ records will be returned by default.

Response
~~~~~~~

.. code-block:: JSON

   [
       {
           "id": "459890698271244288",
           "amount": "0.01",
           "transactionFee": "0",
           "token": "ETH",
           "status": 1,
           "address": "0x386AE30AE2dA293987B5d51ddD03AEb70b21001F",
           "addressTag": "",
           "txId": "0x4ae2fed36a90aada978fc31c38488e8b60d7435cfe0b4daed842456b4771fcf7",
           "applyTime": 1673601139000,
           "network": "ETH",
           "withdrawOrderId": "thomas123",
           "info": "",
           "confirmNo": 100
       },
       {
           "id": "451899190746456064",
           "amount": "0.00063",
           "transactionFee": "0.00037",
           "token": "ETH",
           "status": 1,
           "address": "0x386AE30AE2dA293987B5d51ddD03AEb70b21001F",
           "addressTag": "",
           "txId": "0x62690ca4f9d6a8868c258e2ce613805af614d9354dda7b39779c57b2e4da0260",
           "applyTime": 1671695815000,
           "network": "ETH",
           "withdrawOrderId": "",
           "info": "",
           "confirmNo": 100
       }
   ]
