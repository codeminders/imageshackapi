# METHOD: uploadAndPost #

**http://yfrog.com/api/uploadAndPost**

Note: Now that twitter requires oauth, please use the method outlined here:
**http://code.google.com/p/imageshackapi/wiki/TwitterAuthentication**

Use this method to upload a photo or video to yfrog and to send it as a status update to Twitter.<br />
Request fields<br />
_(post data should be formatted as multipart/form-data)_

  * media - Binary image or video data; either media or url parameter is required
  * url - URL of image or video; either media or url parameter is required
  * username (required) - Twitter username
  * password (required) - Twitter password
  * message (optional) - Message to post to twitter. The URL of the image is automatically added.
  * tags (optional) - comma-separated list of tags. (tags can also include [geo tags](GeoTags.md))
  * public (optional) - Public/private marker of your video/picture. yes means public (default), no means private
  * source (optional) - Twitter **source** parameter to display tweets as 'posted from SOURCE'. If not specified, **yfrog** is used.
  * key - DeveloperKey.


**Sample response:**

```
<?xml version="1.0" encoding="UTF-8"?>
<rsp status="ok">
 <statusid>1111</statusid>
 <userid>11111</userid>
 <mediaid>abc123</mediaid>
 <mediaurl>http://yfrog.com/abc123</mediaurl>
</rsp>
```

**Sample error response:**
```
<?xml version="1.0" encoding="UTF-8"?>
<rsp stat="fail">
    <err code="1001" msg="Invalid twitter username or password" />
</rsp>
```

**Error codes and their descriptions:**<br />
1001 - Invalid twitter username or password<br />
1002 - Image/video not found<br />
1003 - Unsupported image/video type<br />
1004 - Image/video is too big<br />

**URL uploads**

If URL specified in _url_ parameter points to any media located on Imageshack/Yfrog servers (following forms are supported:
  * http://yfrog.com/PATH
  * http://imgX.imageshack.us/imgX/BUCKET/NAME
  * http://imgX.imageshack.us/i/NAME/
  * http://imgX.yfrog.com/i/NAME/
and this media belong to you (caller) then no extra transload will be performed, you'll have a link to the existing media.