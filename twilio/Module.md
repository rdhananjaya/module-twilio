Connects to Twilio from Ballerina. 

# Module Overview

The Twilio connector allows you to send SMS, voice, and OTP messages through the Twilio REST API. You can also send
user secrets via SMS or voice message, verify OTP, and add and delete users. It handles basic authentication.

**Basic Operations**

The `wso2/twilio` module contains operations to get the Twilio account details, send SMS, and make voice calls.

**Authy Operations**

The `wso2/twilio` module contains operations to get Authy app details, add a user, delete a user, get user status, get 
user secret, request OTP via SMS, request OTP via call, and verify OTP.

## Compatibility
|                          |    Version     |
|:------------------------:|:--------------:|
| Ballerina Language       | 0.990.0        |
| Twilio Basic API         | 2010-04-01     |
| Twilio Authy API Version | v1             |

## Sample
First, import the `wso2/twilio` module into the Ballerina project.
```ballerina
import wso2/twilio;
```

**Obtaining Tokens to Run the Sample**

1. Visit [Twilio](https://www.twilio.com/) and create a Twilio Account.
2. Obtain the following credentials from the Twilio dashboard:
    * Account SId
    * Auth Token
    * X Authy API Secret

You can now enter the credentials in the Twilio endpoint configuration.
```ballerina
twilio:TwilioConfiguration twilioConfig = {
    accountSId: config:getAsString(ACCOUNT_SID),
    authToken: config:getAsString(AUTH_TOKEN),
    xAuthyKey: config:getAsString(AUTHY_API_KEY)
};

twilio:Client twilioClient = new(twilioConfig);
```
The `sendSMS` function sends an SMS to a given mobile number from another given mobile number using the specified message.
```ballerina
var details = twilioClient->sendSms(fromMobile, toMobile, message);
if (details is  twilio:SmsResponse) {
    io:println(details);
} else {
    //error
    io:println(details);
}
```
The `addAuthyUser` function adds an Authy user with the given email address, phone number, and country code.
```ballerina
var details = twilioClient->addAuthyUser(email, phone, countryCode);
if (details is  twilio:AuthyUserAddResponse) {
    io:println(details);
} else {
    //error
    io:println(details);
}
```
The `requestOtpViaSms` function sends an OTP SMS to the mobile number of the given user ID.
```ballerina
var details = twilioClient->requestOtpViaSms(userId);
if (details is  twilio:AuthyOtpResponse) {
    io:println(details);
} else {
    //error
    io:println(details);
}
```