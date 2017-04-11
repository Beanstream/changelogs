# sproutPOS EMV SDK for iOS Changelog

## Version 2.3.0

* New sendEmailReceipt API with added paremeter updateEmail (BOOL).  If set to true, the email address will be saved in the system.
```objective-c
- (void)sendEmailReceipt:(NSString * _Nonnull)transactionId
                   email:(NSString * _Nonnull)emailAddress
             updateEmail:(BOOL)updateEmail
                language:(NSString * _Nonnull)language
              completion:(nullable void (^)(BICReceiptResponse * _Nullable response, NSError * _Nullable error))completion;
```
* New ````processTransaction```` API using new ````BICTransactionOptions```` class. The old API has been marked as deprecated.

````objective-c
- (void)processTransaction:(BICTransactionRequest * _Nonnull)request
             transactionOptions:(BICTransactionOptions * _Nonnull)transactionOptions
                     completion:(nullable void (^)(BICTransactionResponse * _Nullable response, NSError * _Nullable error, BOOL updateKeyFile))completion;
````
* New processing option in ````BICTransactionOptions```` added to disable contactless transactions.

* New decline message when chip debit/credit transactions are processed with the wrong card type. 

* Debit encryption keys will update themselves after 20 hours of no initialization, preventing an unwanted declined transaction if the PIN pad was left on for extended periods of time.

* A new error error message "Please try again" instead of "Declined" if debit encryption keys have expired. The next transaction will work as debit keys are automatically updated once expired.

* Added ````terminalType```` parameter to the ````BICCreateSessionResponse```` class.  This parameter indicates if the terminal is unencrypted (1) or encrypted (2).  This SDK can only process encrypted (2) terminal transactions.

* Card holder name will now be saved in the system if it's pulled from the card during a transaction
  * NOTE: This field is automatically populated by the SDK.  Manually inserted values will be overridden.



## Version 2.2.5

* Added terminal ID to API call to allow debit key exchange without rebooting iCMP
* Fixed incorrect name of reversalReason constant. Added panLength as a parameter to ensure status of reversal transactions is 
 displayed correctly. 
