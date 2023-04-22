Webhooks
=========
Webhooks are callback messages from Coins Access to the Merchant, triggered by the events that the Merchant has subscribed to. A webhook contains all relevant information about the event that triggers it.

Webhook Request
---------------

User status update
~~~~~~~~~~~~~~~~~~

.. code-block:: JSON

  {
    "event" : "USER_STATUS_UPDATE",
    "data" : {
      "kycInfo":{
      },
      "kycLevel":"lv2",
      "kycStatus" : "passed"
    }
  }

Response
~~~~~~~~~~

.. code-block:: console

  "OK"    //  "REJECT"
  
**NOTE:** Coins will only push final state events for transaction orders.

Fiat cash-in order status event
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: JSON

  {
    "event" : "FIAT_CASH_IN_NOTIFICATION",
    "data" : {
      "internalOrderId" : 123, // Merchant’s system order number
      "externalOrderId" : 321, // Coins system order number
      "status" : SUCCESS, // order status
      "remarks" : error message, // order status
  }


Response
~~~~~~~~

.. code-block:: console

  "OK"  // If it has another value,  Coins will regard this event as failure

Fiat cash-out order status event
~~~~~~~~

.. code-block:: JSON

  {
    "event" : "FIAT_CASH_OUT_NOTIFICATION",
    "data" : {
      "internalOrderId" : 123, // Merchant’s system order number
      "externalOrderId" : 321, // Coins system order number
      "status" : SUCCESS, // order status
      "remarks" : error message, // order status
  }

P2P transfer event
~~~~~~~~~~~~~~~~~~~

.. code-block:: JSON

  {
    "event" : "FIAT_P2P_TRANSFER_NOTIFICATION",
    "data" : {
      "clientTxId":"abc001", // Merchant’s system transfer request id
       "fromUserId":"10001",
       "toUserId" : "10002",
       "amount" : "10",
       "currency" : "PHP"
       "status":"success", //success, failed
       "remarks": "" //enum
  }
  //if status=failed, remarks will return enum of failed reason

Batch transfer event
~~~~~~~~~~~~~~~

.. code-block:: JSON

  {
    "event" : "FIAT_BATCH_TRANSFER_NOTIFICATION",
    "data" : {
       "batchTxId":"abc001", // Merchant’s system transfer request id
       "fromUserId":"10001",
       "toUserId" : "10002",
       "amount" : "10",
       "currency" : "PHP"
       "status":"success", //success, failed
       "remarks": "" //enum
  }
  //if status=failed,remarks will return enum of failed reason

Balance change event
~~~~~~~~~~~~~~~

.. code-block:: JSON

  {
    "event" : "BALANCE_CHANGE_EVENT",
    "data" : {
       "userId":"10001",
       "currency" : "PHP"
       "available" : "10", 
       "locked"  :  "2000",
       "unconfirmed"  :  "2000",
       "changed" : "10", // changed amount from available balance   
       "type":"DEPOSIT", //DEPOSIT, WITHDRAW, TRANSFER
       "clientTxId": ""  //clientTxId
       "time": 1675225144301  //timestamp, millis
  }
  //Push this event when available balance is changed. Positive number means credit, and negative number means debit.

Response
~~~~~~~~~~~~~~~

.. code-block:: console

  "OK"  // If it has another value,  Coins will treat this event as a failure.
  
Event Enums

.. code-block:: console
  USER_STATUS_UPDATE
  TRANSACTION_STATUS_UPDATE
  FIAT_CASH_IN_NOTIFICATION
  FIAT_CASH_OUT_NOTIFICATION
  FIAT_P2P_TRANSFER_NOTIFICATION
  FIAT_BATCH_TRANSFER_NOTIFICATION
  BALANCE_CHANGE_EVENT
