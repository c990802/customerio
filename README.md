#Customer.io Node Client

Clean and simple NodeJS wrapper for the Customer.io [REST API](http://customer.io/docs/api/rest.html). 
Designed specifically to be as similar as possible to the main Customer.io [JavaScript client](http://customer.io/docs/javascript-quick-start.html).

##Installation

```
npm install node-customerio --save
```

##Example

```js
var customer = require('node-customerio');

// Configure the module to your account
customer.init('your_site_id', 'your_api_key');

// Identify a user 
customer.identify({
  id: '123',
  email: 'billy@jean.com',
  created_at: new Date(2014, 09, 24) // can also pass UNIX timestamp here
});

// Delete a user
customer.delete('123');

// Track an event for a user
customer.track('123', 'boughtPingPongPaddle', {
  color: 'red'
});
```

***

##Methods

###customer.init(siteId, apiKey)

Set up the the module to work with your account by inputting your `siteId` and `apiKey`.

```js
customer.init('your_site_id', 'your_api_key');
```

###customer.identify(properties)

Create/update a user in Customer.io, passing any properties. 

Note: JavaScript dates are automatically converted to UNIX to comply with Customer.io's standard of timestamp policy.

Returns a [When-style](https://github.com/cujojs/when) promise.

```js
customer.identify({
  id: '123',
  email: 'chris@test.com',
  created_at: new Date(2014, 09, 24), // can also pass UNIX timestamp here
  steven: 'smith'
}).done(function (result) {
  console.log('done');
}, function (err) {
  console.log('oh noes!', err);
});
```

###customer.remove(customerId)

Removes a customer by id. 

Returns a [When-style](https://github.com/cujojs/when) promise.

```js
customer.remove('547243166e8e449111f866bb').done(function () {
  console.log('done');
}, function (err) {
  console.log(err);
});
```

###customer.track(customerId, eventName, properties)

Track an event for a given customer. `properties` are optional. 

Note: JavaScript dates are automatically converted to UNIX to comply with Customer.io's standard of timestamp policy.

Returns a [When-style](https://github.com/cujojs/when) promise.

```js
customer.track('123', 'boughtPingPongPaddle', { color: "red" }).done(function () {
  console.log('done');
}, function (err) {
  console.log('oh no', err);
});
```

***

##Why was this library built?

There is a [recommended library](https://github.com/liamdon/node-customer.io) which throws errors.
Throwing errors is bad. Plus, [When.js](https://github.com/cujojs/when) promises are the shizz for handling async flow.

Oh, and Customer.io is awesome, obviously! 

***

##Licence

Released under the MIT license. See file called [LICENCE](LICENCE) for more details.