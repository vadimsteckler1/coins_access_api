API Specification
=================

This section outlines all the needed information and endpoints that are required to perform the available actions.

Common Headers
---------------

The table below shows all of the common API Headers you will encounter in the Coins Access API.

.. table::
================ ========== ======= =========== ===============================================
Header Name      Required   Type    Example     Description                                   
================ ========== ======= =========== ===============================================
X-Merchant-Key   yes        string              The authorized merchant key 
X-Merchant-Sign  yes        string              The authorized merchant request sign           
X-Timestamp      yes        long    1671158910  Request initiation time                       
X-Trace-Id       no         string              Request log trace ID                          
================ ========== ======= =========== ===============================================

To craft an X-Merchant-Sign:

1. Construct a message according to the following pseudo-grammar: 'X-Timestamp' + URL(http://192.168.0.1/merchant-api/account?paramKey=paramValue&paramKey2=paramValue2) + BODY(key1=value1&key=value2)
2. Calculate an HMAC with the message string you just created, your API secret as the key, and SHA256 as the hash algorithm.
