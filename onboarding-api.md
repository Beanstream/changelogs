# Onboarding API Change Log
## Reflects backwards-incompatible updates:

## 2016-08-18
        - Add Personal Guarantee Accepted to agreement all flows (optional)
        - PSP CAD: Business Currency is removed
        - PSP CAD: Owners is no longer required
        - PSP CAD: business.has_exising_account is removed
        - PSP CAD: business.owners minimum items changed from 1 to 0
        - PSP CAD: business.owners.percentage has been removed
        - Pending Issues now has a message property: A human readable message about the error
        - Pending Issues renamed field -> name
        - Pending Issues renamed code -> reason
        - Error responses renamed field -> name
        - Error responses renamed code -> reason
        - Error response added message property
        - EFT CAD: email becomes required
        - EFT CAD: date of birth is **new** and is required
        - EFT CAD: directors is no longer required
        - EFT CAD: services description is **new** and required
        - EFT CAD: directors start_date is removed
        - EFT CAD: directors percentage is removed

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

## 2016-06-10
    - First release of the api specification
