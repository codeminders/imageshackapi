You can use unix  [curl(1)](http://curl.haxx.se/) utility to access ImageShack/Yfrog APIs.

## Yfrog ##

Upload and post a picture:

```
  curl -F "media=@file.png;type=image/png" -F username=user -F password=pass -F key=key http://yfrog.com/api/uploadAndPost
```

Upload and post a video:

```
  curl -F "media=@file.mp4;type=video/quicktime" -F username=user -F password=pass -F key=key http://yfrog.com/api/uploadAndPost
```

## ImaheShack ##

Coming soon...