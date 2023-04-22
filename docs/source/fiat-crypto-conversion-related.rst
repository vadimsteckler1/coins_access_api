Fiat-Crypto Conversion Related Endpoints
========================================

The methods described in this section enable real-time currency conversion between fiat and crypto. 
Each endpoint facilitates a specific use case. Users only need to select the current currency and target currency, then accept the quote, and quickly obtain the target currency.

System Integration
-----------------

.. image::
   fiat-crypto.png

.. image::
   fiat-crypto-business.png

Retrieving Supported Trading Pairs
~~~~~~~~~~~~~~~~~~~~~~~~

This constantly updated endpoint returns all available trading pairs. Response details include the minimum and maximum source amounts and the source currency precision in decimal places. 

**API Type:** HTTP

**Method:** POST

**URL:** /merchant-api/convert/get-supported-trading-pairs

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
     - no
     - User ID in Coins

Response
~~~~~~~

.. code-block:: JSON

  {
      "status": 0,
      "error": "OK",
      "data":[
          {
              "sourceCurrency":"PHP",
              "targetCurrency":"BTC",
              "minSourceAmount":"1000",
              "maxSourceAmount":"15000",
              "precision" : "2"           
          },
          {
              "sourceCurrency":"BTC",
              "targetCurrency":"PHP",
              "minSourceAmount":"0.0001",
              "maxSourceAmount":"0.1",
              "precision" : "8"
          },
          {
              "sourceCurrency":"PHP",
              "targetCurrency":"ETH",
              "minSourceAmount":"1000",
              "maxSourceAmount":"18000",
              "precision" : "2"
          },
          {
              "sourceCurrency":"ETH",
              "targetCurrency":"PHP",
              "minSourceAmount":"0.003",
              "maxSourceAmount":"4.2",
              "precision" : "8"
          }
      ]
  }

Fetching a Quote
~~~~~~~~~~~~~~~~~~~~~~~~

This endpoint returns a quote for specified ``sourceCurrency`` and ``targetCurrency``.

**API Type:** HTTP

**Method:** POST

**URL:** /merchant-api/convert/get-quote

Request
~~~~~~~

.. list-table::
   :header-rows: 1
   
   * - Parameter
     - Layout
     - Required
     - Description
   * - sourceCurrency
     - Request body
     - yes
     - The currency the user holds
   * - targetCurrency
     - Request body
     - yes
     - The currency the user would like to obtain
   * - sourceAmount
     - Request body
     - yes
     - The amount of the source currency    

Sample request
~~~~~~~

**NOTE**: To convert PHP, use 0.1 BTC

.. code-block:: JSON

  {
      "sourceCurrency":"BTC",
      "targetCurrency": "PHP",
      "sourceAmount" : "0.1"
  }

Response
~~~~~~~

.. code-block:: JSON

  {
     "status": 0,
      "error": "OK",
      "data": {
          "quoteId": "2182b4fc18ff4556a18332245dba75ea",
          "sourceCurrency": "BTC",
          "targetCurrency": "PHP",
          "sourceAmount": "0.1",
          "price": "59999",             //1BTC=59999PHP
          "targetAmount": "5999",       //The amount of PHP the user holds
          "expiry": "10"
      }
  }

Accepting a Quote
~~~~~~~~~~~~~~~~~~~~~~~~

This endpoint accepts the quote obtained using the ``get-quote`` method.

**API Type:** HTTP

**Method:** POST

**URL:** /openapi/convert/v1/accept-quote

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
     - User ID in Coins
   * - sourceCurrency
     - Request body
     - yes
     - The currency the user holds
   * - targetCurrency
     - Request body
     - yes
     - The currency the user would like to obtain
   * - sourceAmount
     - Request body
     - yes
     - The amount of the source currency
   * - quoteId
     - Request body
     - yes
     - The ID assigned to the quote    

Response
~~~~~~~

.. code-block:: JSON

  {
      "status": 0,
      "data": {
          "orderId" : "49d10b74c60a475298c6bbed08dd58fa"
          "success": true
      },
      "error": "ok"
  }



