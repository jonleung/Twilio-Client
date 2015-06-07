# Instructions


0) Recognize that if you use this library, anyone who looks at your webpage will be able to use your Twilio account SID and auth token.

1) In `twilio_client.js`, modify lines 1&2

```js
var TWILIO_ACCOUNT_SID = "XXX";
var TWILIO_AUTH_TOKEN = "YYY";
```

so that it has your actual Twilio Account SID and Auth Token.

2) Use the rest of the library as it were the [twilio node library](http://twilio.github.io/twilio-node/) except that the variable `client` is already defined for you because we will have already run this line for you:

```js
var client = require('twilio')('ACCOUNT_SID', 'AUTH_TOKEN');
```

so know this should work (note, currently untested)

```js
//Send an SMS text message
client.sendMessage({

    to:'+16515556677', // Any number Twilio can deliver to
    from: '+14506667788', // A number you bought from Twilio and can use for outbound communication
    body: 'word to your mother.' // body of the SMS message

}, function(err, responseData) { //this function is executed when a response is received from Twilio

    if (!err) { // "err" is an error received during the request, if any

        // "responseData" is a JavaScript object containing data received from Twilio.
        // A sample response from sending an SMS message is here (click "JSON" to see how the data appears in JavaScript):
        // http://www.twilio.com/docs/api/rest/sending-sms#example-1

        console.log(responseData.from); // outputs "+14506667788"
        console.log(responseData.body); // outputs "word to your mother."

    }
});

//Place a phone call, and respond with TwiML instructions from the given URL
client.makeCall({

    to:'+16515556677', // Any number Twilio can call
    from: '+14506667788', // A number you bought from Twilio and can use for outbound communication
    url: 'http://www.example.com/twiml.php' // A URL that produces an XML document (TwiML) which contains instructions for the call

}, function(err, responseData) {

    //executed when the call has been initiated.
    console.log(responseData.from); // outputs "+14506667788"

});
```