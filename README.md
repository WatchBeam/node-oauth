node-oauth
===========
A simple OAuth API for node.js. This API allows users to authenticate against OAuth providers, and thus act as OAuth consumers. It also has support for OAuth Echo, which is used for communicating with 3rd party media providers such as TwitPic and yFrog.

Tested against [Twitter](http://twitter.com), [term](http://term.ie/oauth/example/), TwitPic, and Yahoo!

Also provides rudimentary OAuth2 support, tested against Facebook, GitHub, Foursquare, Google and Janrain.  For more complete usage examples please take a look at [connect-auth](http://github.com/ciaranj/connect-auth)

Installation
==============

  `npm install oauth`


Examples
==========

To run examples/tests install Mocha `npm install -g mocha` and run `mocha your-file-name.js`:

## OAuth1.0

```javascript
describe('OAuth1.0',function(){
 var OAuth = require('oauth');

 it('tests trends Twitter API v1.1',function(done){
  var oauth = new OAuth.OAuth(
   'https://api.twitter.com/oauth/request_token',
   'https://api.twitter.com/oauth/access_token',
   'your application consumer key',
   'your application secret',
   '1.0A',
   null,
   'HMAC-SHA1'
  );
  oauth.get(
   'https://api.twitter.com/1.1/trends/place.json?id=23424977',
   'your user token for this app', //test user token
   'your user secret for this app', //test user secret
   function (e, data, res){
    if (e) console.error(e);    
    console.log(require('util').inspect(data));
    done();
   });
 });
});
```

## OAuth2.0
```javascript
describe('OAuth2',function(){
 var OAuth = require('oauth');

  it('gets bearer token', function(done){
   var OAuth2 = OAuth.OAuth2;
   var twitterConsumerKey = 'your key';
   var twitterConsumerSecret = 'your secret';
   var oauth2 = new OAuth2(server.config.keys.twitter.consumerKey,
    twitterConsumerSecret,
    'https://api.twitter.com/',
    null,
    'oauth2/token',
    null);
   oauth2.getOAuthAccessToken(
    '',
    {'grant_type':'client_credentials'},
    function (e, access_token, refresh_token, results){
    console.log('bearer: ',access_token);
    done();
   });
  });
```