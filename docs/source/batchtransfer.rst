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
