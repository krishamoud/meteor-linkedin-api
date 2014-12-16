meteor-linkedin
==============

Linkedin wrapper for meteor
Thanks to [Hamza Waqas](https://github.com/ArkeologeN) for his [node-linkedin](https://github.com/ArkeologeN/node-linkedin) package which this is forked from

### Getting Started

Add `khamoud:linkedin-api` to your application's `.meteor/packages` file

Alternatively:
```
meteor add khamoud:linkedin-api
```

Before invoking any endpoint, please get the instance ready with your access token.
This is assuming that you already have access to an access token from a linkedin login


```javascript
var linkedin = Linkedin().init('my_access_token');
// Now, you're ready to use any endpoint
```

Additionally, you can specify options. Currently, the only supported option is `timeout`, allowing you to specific a timeout (in ms) for the HTTP request. The default is 60 seconds (a value of 60000).

```javascript
var linkedin = Linkedin.init('my_access_token', {
    timeout: 10000 /* 10 seconds */
});
```


## Companies

Supports all the calls as per the documentation available at: [LinkedIn Companies API](http://developer.linkedin.com/documents/company-lookup-api-and-fields).

```javascript
linkedin.companies.company('162479', function(err, company) {
    // Here you go
});

linkedin.companies.name('logica', function(err, company) {
    // Here you go
});

linkedin.companies.email_domain('apple.com', function(err, company) {
    // Here you go
});

linkedin.companies.multiple('162479,universal-name=linkedin', function(err, companies) {
    // Here you go
});

linkedin.companies.asAdmin(function(err, companies) {
    // Here you go
});
```

## Profile

Searches for the profiles as per the criteria.

### Logged In User Profile.

```javascript
linkedin.people.me(function(err, $in) {
    // Loads the profile of access token owner.
});

OR

linkedin.people.me(['id', 'first-name', 'last-name'], function(err, $in) {
    // Loads the profile of access token owner.
});
```

### Profile by Public URL.

```javascript
linkedin.people.url('long_public_url_here', function(err, $in) {
    // Returns dob, education
});

OR

linkedin.people.url('long_public_url_here', ['id', 'first-name', 'last-name'], function(err, $in) {
    // Returns dob, education
});
```

### Profile by Id.

```javascript
linkedin.people.id('linkedin_id', function(err, $in) {
    // Loads the profile by id.
});

OR

linkedin.people.id('linkedin_id', ['id', 'first-name', 'last-name'], function(err, $in) {
    // Loads the profile by id.
});

```

## Connections

Invokes LinkedIn's Connections API.

```javascript
linkedin.connections.retrieve(function(err, connections) {
    // Here you go! Got your connections!
});

```

## Groups

Implements wrapper for `LinkedIn Group API` and provides interface to invoke API endpoints.

PS: For now, we just have feeds available.

### Group discussions by Group ID
```javascript
linkedin.group.feeds(3769732, function(err, data) {
    // data: variable is ready to use.
});
```

OR If you want to have custom field selector, take a look at this;

```javascript
linkedin.group.feeds(3769732, ['field', 'field2', 'field3'] , function(err, data) {
    // data: variable is ready to use.
});
```

OR even if you want to have custom sorting parameters, you can just pass them as third argument:

```javascript
linkedin.group.feeds(3769732, ['field', 'field2', 'field3'], {order: 'popularity'}, function(err, data) {
    // data: variable is ready to use.
});
```

## Author

The original wrapper was written & currently under maintenance by [Hamza Waqas](http://github.com/ArkeologeN). He's using twitter at: [@HamzaWaqas](http://twitter.com/HamzaWaqas)
