# How to authenticate using Twitter OAuth credentials #

# Introduction #

We have created a new upload method that uses Twitter Echo OAuth, here is how to use it:

Send all OAuth upload requests using POST to:

http://yfrog.com/api/xauth_upload
or
https://yfrog.com/api/xauth_upload

### Requirements ###
```
media (filename required)
key (your api key required)
```

X-Auth-Service-Provider:
https://api.twitter.com/1/account/verify_credentials.xml
(only XML is supported at this time).

You will need a header for authorization, here is it:

X-Verify-Credentials-Authorization:
```
OAuth realm="http://api.twitter.com/",
oauth_consumer_key="",
oauth_signature_method="HMAC-SHA1",
oauth_token="",
oauth_timestamp="",
oauth_nonce="",
oauth_version="1.0",
oauth_signature=""
```

Here is a sample POST from php via command line:
```
# php yfrog_test.php ./test.jpg

[jack@zero ~]$ php yfrog_test.php ./test.jpg

* About to connect() to yfrog.com port 80 (#0)
*   Trying 208.94.0.29... * connected
* Connected to yfrog.com (208.94.0.29) port 80 (#0)
> POST /api/xauth_upload HTTP/1.1
Host: yfrog.com
Accept: */*
X-Auth-Service-Provider:
https://api.twitter.com/1/account/verify_credentials.xml
X-Verify-Credentials-Authorization:
oauth_consumer_key="kgmLtpVA6ipyBcePT7MKaQ",
oauth_nonce="6c893cf4adb9f9d28aadc86b16fe837b",
oauth_signature="U7KgIJPBtaEtRN8BfxTRFVoL9kE%3D",
oauth_signature_method="HMAC-SHA1", oauth_timestamp="1274651607",
oauth_token="139881639-MePpdaz3Kvz6WuOeKFeQgLOdg3f54gVMGXcQRryY",
oauth_version="1.0"
Content-Length: 923876
Expect: 100-continue
Content-Type: multipart/form-data;
boundary=----------------------------a21ff70823f9
* Closing connection #0

Response is:

<?xml version="1.0" encoding="UTF-8"?>
<rsp stat="ok">
<mediaid>af11zj</mediaid>
<mediaurl>http://yfrog.com/af11zj</mediaurl>
</rsp>
```
In which case an image was uploaded to the User's YFrog account.


API below this line is going to continue to work, but we recommend using the API described above



If user have been already authenticated using OAuth,  when posting images to YFrog on his behalf (using ['upload'](http://code.google.com/p/imageshackapi/wiki/YFROGupload) method) you may want to pass his identity, so later on he can manage and delete his posted images at Yfrog web site.

See working example (PHP) here:
http://imageshackapi.googlecode.com/files/upload-to-yfrog-example-with-xauth.php

# Old oauth request method api #

When you are using unified upload API, you can pass following parameters:

  * auth=**oauth**
  * username - twitter username
  * verify\_url - a signed URL that points to twitter's vertify\_credentials page in form:

```
https://twitter.com/account/verify_credentials.xml?oauth_version=1.0&oauth_nonce=NONCE&oauth_timestamp=STAMP&oauth_consumer_key=CONSUMER_KEY&oauth_token=TOKEN&oauth_signature_method=HMAC-SHA1&oauth_signature=SIGNATURE
```

The request must be signed using your Twitter OAuth credentials and user Token.

We'll check if account described by OAuth parameters is the same as specified in _a\_username_ and will use this information to link a picture or video to user's account.

Then, user can manage all hist posted images/videos at

`http://yfrog.com/froggy.php?username=TWITTER_USERNAME`

See working example (PHP) here:
http://imageshackapi.googlecode.com/files/upload-to-yfrog-example.php