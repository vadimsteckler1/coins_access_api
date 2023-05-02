Webhooks
=========
Webhooks are callback messages from Coins Access to the Merchant, triggered by the events that the Merchant has subscribed to. A webhook contains all relevant information about the event that triggers it.

Webhook Request
---------------

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
