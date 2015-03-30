# METHOD: uploadToWozai #

**http://yfrog.com/api/uploadToWozai**

Use this method to upload a photo or video to yfrog using your Wozai [Wozai.cc](http://wozai.cc/) credentials.<br />
Request fields<br />
_(post data should be formatted as multipart/form-data)_

  * media - Binary image or video data; either media or url parameter is required
  * url - URL of image or video; either media or url parameter is required
  * username (required) - Wozai username
  * password (required) - Wozai password
  * tags (optional) - comma-separated list of tags. (tags can also include [geo tags](GeoTags.md))
  * public (optional) - Public/private marker of your video/picture. yes means public (default), no means private
  * key - DeveloperKey.


**Sample response:**

```
<?xml version="1.0" encoding="UTF-8"?>
<rsp stat="ok">
<mediaid>e4ht1p</mediaid>
<mediaurl>http://yfrog.com/e4ht1p</mediaurl>
</rsp>
```

**Sample error response:**
```
<?xml version="1.0" encoding="UTF-8"?>
<rsp stat="fail">
<err code="1001" msg="Invalid username or password specified"/>
</rsp>
```

**Error codes and their descriptions:**<br />
1001 - Invalid Wozai username or remote key<br />
1002 - Image/video not found<br />
1003 - Unsupported image/video type<br />
1004 - Image/video is too big<br />

**NOTE: this method is experimental and might change in future without notice!**