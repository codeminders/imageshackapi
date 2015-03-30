# METHOD: upload #

**http://yfrog.com/api/upload**

Use this method if you only want to upload a photo or video to yfrog.<br />
Request fields<br />
_(post data should be formatted as multipart/form-data)_

  * media - Binary image or video data; either media or url parameter is required
  * url - URL of image or video; either media or url parameter is required.
  * username (required) - Twitter username
  * password (required) - Twitter password
  * tags (optional) - comma-separated list of tags. (tags can also include [geo tags](GeoTags.md)])
  * public (optional) - Public/private marker of your video/picture. yes means public (default), no means private
  * key - DeveloperKey.


**Sample response:**

```
<?xml version="1.0" encoding="UTF-8"?>
<rsp stat="ok">

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