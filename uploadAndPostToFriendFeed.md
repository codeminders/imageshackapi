# METHOD: uploadAndPostToFriendFeed #

**http://yfrog.com/api/uploadAndPostToFriendFeed**

Use this method to upload a photo or video to yfrog and to send it as an update to [FriendFeed](http://FriendFeed.com/).<br />
Request fields<br />
_(post data should be formatted as multipart/form-data)_

  * media - Binary image or video data; either media or url parameter is required
  * url - URL of image or video; either media or url parameter is required
  * username (required) - FriendFeed username
  * password (required) - FiendFeed "Remote Key" (could be acquired [here](https://friendfeed.com/account/api) )
  * message (optional) - Message to post to FriendFeed. The URL of the image is automatically added.
  * tags (optional) - comma-separated list of tags. (tags can also include [geo tags](GeoTags.md))
  * public (optional) - Public/private marker of your video/picture. yes means public (default), no means private
  * key - DeveloperKey.


**Sample response:**

```
<?xml version="1.0" encoding="UTF-8"?>
<rsp stat="ok">
<statusid>53c41e9f-8300-40a4-a444-c2c57a413134</statusid>
<userid>ed9138ed-f080-4bc4-bb0b-10619e60c473</userid>
<mediaid>5dw6ej</mediaid>
<mediaurl>http://yfrog.com/5dw6ej</mediaurl>
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
1001 - Invalid FriendFeed username or remote key<br />
1002 - Image/video not found<br />
1003 - Unsupported image/video type<br />
1004 - Image/video is too big<br />

**NOTE: this method is experimental and might change in future without notice!**