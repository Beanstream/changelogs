# Onboarding API Change Log

## Release Date: November 28, 2016
### API version 2016-08-18
#### GW-USA
- New Gateway USA spec added


## Release Date: November 16, 2016
### API version 2016-08-18
#### PSP-USD
- Extensive changes to spec (see developer docs for more details http://developer.beanstream.com/documentation/onboarding-api-reference/)

#### GW-CDN
- New Gateway Canadian spec added

## Release Date: September 10, 2016

### All API version Changes
* File name on get response now includes the file type extension
* API Version 2016-06-10 Deprecated and will be removed in the next release

### Introduced API version 2016-08-18
#### Common changes for all workflows
* Agreement.personal_guarantee_accepted is **new** and is optional
 Although optional the personal guarantee must be accepted where entity_type is "sole_proprietor"  
  or "partnership"
* Remove restriction on country fields so that full ISO 3166 list of country codes can be accepted
* Address.region and Address.postal_code are now optional
* pending_issues.message is new and contains a human readable message about the error
* Error responses has renamed field error.name
* Error responses has renamed field error.reason
 Error.message is new and contains a human readable message about the error

#### PSP CAD
* PspCadOwner all fields are now optional
 Although optional PspCadOwner fields must be supplied where PspCadBusiness.entity_type is "non_profit"  
 or "corporation" 
* PspCadBusiness.has_exising_account is removed
* PspCadOwners.percentage is removed
* PspCadBusiness.currency is removed
        
#### EFT CAD
* EftCadDirector all fields are now optional
* Although optional EftCadDirector fields must be supplied where EftCadBusiness.entity_type is "non_profit"  
  or "corporation" or "publically_traded"
* EftCadDirector.start_date is removed
* EftCadDirector.percentage is removed
* EftApplicant.email is now required
* EftCadApplicant.date_of_birth is **new** and required
* EftCadBusiness.services_description is **new** and required
        
        
## Release Date: June 11, 2016        
## 2016-06-11
###  API version is now required in the header attributes X-API-Version: 2016-06-11
        - Additional Properties is now set to False
            This means that no extra/undefined properties will be allowed to be passed in that are not already in the swagger specification.
        - API Global Address changes
        Allow sign up for payments in a country where the head office address is not domiciled in the same location
        Users of the onboarding API can submit addresses from countries outside of the currently defined regions.
        Update the API to allow for a more generic and universal address object.

        - The list of Countries for each flow is now more extensive for each of the flow a large list of countries is available.
        - Postal Code is no longer a required field.
        - Region is now being collected in all flows, it was an enum in previous specific flows for provinces and is now a string maxlength 64
        - Global Address Fields would replace all existing address fields as follows:
            - Address line 1
            - Address line 2
            - Region (includes: state/province/municipality/region)
            - City
            - Postal Code (includes ZipCode)
            -- Country
        - PSP US Flow: Social Security Number is now required.


## Release Date: June 10, 2016  
## 2016-06-10
    - First release of the api specification
    
