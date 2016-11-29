# sproutPOS EMV SDK for Android Changelog

## Version 2.3.0

* New BeanstreamAPI call for processing transactions
 * public void processTransaction(TransactionRequest transactionRequest, TransactionOptions transactionOptions) 
* New TransactionOptions which dictate how the iCMP will function.
 * public TransactionOptions(int mode)
 * public TransactionOptions(int mode, int[] tipPresets) {
 * MODE_DEFAULT -> Insert, Swipe and Contactless Transactions
 * MODE_NO_CONTACTLESS -> Insert and swipe transactions
 * MODE_TIPS_NO_CONTACTLESS -> Insert and swipe with tips functionality.
* processTransaction() will return a TransactionError.INVALID_TRANSACTION_MODE if you submit an invalid mode to the new TransactionOptions object and process a transaction.
* The following has been deprecated in favor of the new processTransaction method. 
 * ProcessTransaction(final TransactionRequest transactionRequest, final boolean isTipsEnabled, final int[] tipPresets) {
* New BeanstreamAPI call for sending emails
 * public void sendEmailReceipt(String transactionId, String email, boolean updateEmail, String language)
 * If updateEmail is set to true, records the email on the transaction in our database.
* The PaymentMethods object has a new method getFullName(String paymentMethod).
 * e.g. getFullName(PaymentMethods.DEBIT) -> "Debit"	
* The TransactionTypes object has a new method getFullName(String TransactionTypes).
 * e.g. getFullName(TransactionTypes.PURCHSE) -> "Purchase"
* Processing a chip/contactless debit transaction with a credit card, will return "NOT A DEBIT CARD" in the declined message.
* Processing a chip/contactless credit transaction with a debit card, will return "NOT A CREDIT CARD" in the declined message.
* If debit transactions decline due to invalid encryption keys, the response will indicate to try again as the SDK automatically retrieves new keys.
* Debit encryption keys will now automatically get updated after 20 hours if the iCMP has not been powered off.
* SearchTransactionResponse object now has an isApproved() method to determine if the transaction was approved or not.
* SearchTransactionResponse now has a notes field. This returns data if transactionRequest.setOrder_notes(String) was used when processing the transaction.

Additionally, a few changes were made to the SDK to improve user experiences of merchants with multiple Beanstream merchant account types. This SDK only works with Beanstream merchant accounts that have an encrypted terminal set up (for use with the iCMP EMV solution). Some Beanstream merchants have encrypted (iCMP EMV) merchant accounts and unencrypted (e-commerce) merchant accounts. If merchants log in with the wrong Beanstream merchant account credentials they will be able to create a session using the Beanstream API, but will not be able to use your solution integrated with the EMV SDK. This leads to confusion, and processing errors when attempting transactions.

To help resolve this issue we've added a couple checks in the SDK and added a new method.

* BeanstreamAPI.isTerminalTypeEncrypted() returns true if the merchant account that is logged in has an encrypted terminal. If this is true, then everything is good. If it's false, we recommend showing a dialog advising the user that the account they are using is not supported.

* Processing transactions and PIN pad initialization in the SDK will now only work if the merchant account has an encrypted terminal. Attempting to initialize the PIN pad or process a transaction will result in a TERMINAL_NOT_ENCRYPTED error.

### Bug Fixes

* Fixed an issue where terminal IDs were not resetting correctly internally. If you log into a new merchant account, or anytime the pin pad service is started, the memory is cleared and the value retrieved again. This was impacting customers with multiple merchant accounts.


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
