# sproutPOS EMV SDK for Android Changelog
## Version 2.2.0

* Initial support for multi-terminal use on a single Android device.  See documentation for changes. 
* Now validating transaction amounts before allowing them to be processed. Will return a TransactionError with error code 
 TransactionError.INVALID_TRANSACTION_AMOUNT
* Updated the TransactionError error message if you attempt to process an EMV transaction and the iCMP is not connected
* TransactionRequest.setEmvEnabled(boolean) is now removed.  It will now be automatically detected based off
 the payment method used (specifically PaymentMethods.DEBIT_EMV and PaymentMethods.CREDIT_EMV)
* Calling BeanstreamAPI.processTransaction(request) will no longer return an additional InitCardReaderResponse event.  
  It will still attempt to initialize the PIN pad before every transaction, but any error will come back as a TransactionError event.  
   TransactionResponse.isUpdatekeyEncryption() is now available and can be used to check if your pin pad requires an update, in addition to checking InitCardReaderResponse if you initialize the PIN pad manually
* Added interfaces for all BeanstreamAPI events.  While not required to receive an event, they can help ensure you've implemented all the required event receivers, and don’t miss any required changes. These are available in the BeanstreamEvents class.  See documentation for full list of interfaces   
* Products can now be added to the TransactionRequest's inventoryItemList
* New DiscountType object in SDK and discount fields on the TransactionRequest object (these values don't get submitted 
to API and are informational only, but can be used to keep the entire request information in one spot)

### Bug Fixes

* Fixed an issue where some contactless transactions would reverse incorrectly
* Fixed OOM issue if retrofit pulled down an extremely large file
* Fixed rounding issue on small tip amounts
* Fixed problem on contactless transactions if card type was not an accepted card type.  
 The transaction will fail correctly now
* TransactionRequest sub_total field is now submitted to the API, is used for display purposes only
* CreateSessionWithSavedCredentials had an occasionally long running action before it was threaded, it's now threaded immediately
* Fixed crash that could occur when using the keystore for user credentials
