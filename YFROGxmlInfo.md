# METHOD: xmlInfo #

**http://yfrog.com/api/xmlInfo**

_Parameters:_

**path** - path part of yfrog image/video URL.

For example for
```
http://yfrog.com/0g6i6xv3j
```
The call would be
```
http://yfrog.com/api/xmlInfo?path=0g6i6xv3j
```
<br />
Result is XML document like this:
```
<?xml version="1.0" encoding="iso-8859-1"?>
<imginfo xmlns="http://ns.imageshack.us/imginfo/6/" version="6" timestamp="1234911746">
  <rating>
    <ratings>0</ratings>
    <avg>0.0</avg>
  </rating>
  <files server="16" bucket="733">
     <image size="189113" content-type="image/jpeg">6i6xv3.jpg</image>
     <thumb size="5889" content-type="image/jpeg">6i6xv3.th.jpg</thumb>
  </files>
  <resolution>
    <width>410</width>
    <height>500</height>
  </resolution>
  <class>r</class>
  <uploader>
  </uploader>
  <links>
    <image_link>http://img16.imageshack.us/img16/733/6i6xv3.jpg</image_link>
    <image_html><a href="http://img16.imageshack.us/my.php?image=6i6xv3.jpg" target="_blank"><img 
    src="http://img16.imageshack.us/img16/733/6i6xv3.jpg" alt="Free Image Hosting at www.ImageShack.us" 
    border="0"/></a></image_html>
    <image_bb>[URL=http://img16.imageshack.us/my.php?image=6i6xv3.jpg]
    [IMG]http://img16.imageshack.us/img16/733/6i6xv3.jpg[/IMG][/URL]</image_bb>
    <image_bb2>[url=http://img16.imageshack.us/my.php?image=6i6xv3.jpg]
    [img=http://img16.imageshack.us/img16/733/6i6xv3.jpg][/url]</image_bb2>
    <thumb_link>http://img16.imageshack.us/img16/733/6i6xv3.th.jpg</thumb_link>
    <thumb_html><a href="http://img16.imageshack.us/my.php?image=6i6xv3.jpg" target="_blank">
    <img src="http://img16.imageshack.us/img16/733/6i6xv3.th.jpg" alt="Free Image Hosting at www.ImageShack.us" 
    border="0"/></a></thumb_html>
    <thumb_bb>[URL=http://img16.imageshack.us/my.php?image=6i6xv3.jpg]
    [IMG]http://img16.imageshack.us/img16/733/6i6xv3.th.jpg[/IMG][/URL]</thumb_bb>
    <thumb_bb2>[url=http://img16.imageshack.us/my.php?image=6i6xv3.jpg]
    [img=http://img16.imageshack.us/img16/733/6i6xv3.th.jpg][/url]</thumb_bb2>
    <ad_link>http://img16.imageshack.us/my.php?image=6i6xv3.jpg</ad_link>
    <done_page>http://img16.imageshack.us/content.php?page=done&l=img16/733/6i6xv3.jpg</done_page>
  </links>
</imginfo>
```

For video files result is XML document like this:
```
<?xml version="1.0" encoding="ISO-8859-1"?>
<imginfo xmlns="http://ns.imageshack.us/imginfo/7/" version="7" timestamp="1243036600">
  <rating>
    <ratings>0</ratings>
    <avg>0.0</avg>
  </rating>
  <files server="190" bucket="6189">
     <image size="197679" content-type="video/mp4">samplew.mp4</image>
     <thumb size="1258" content-type="image/jpeg">samplew.mp4.th.jpg</thumb>
     <frame size="6523" content-type="image/jpeg">samplew.mp4.frm.jpg</frame>
  </files>
  <resolution>
    <width>480</width>
    <height>318</height>
  </resolution>
  <video-info>
    <status>complete</status>
    <duration>4000</duration>
  </video-info>
  <class>r</class>
  <visibility>no</visibility>
  <uploader>
    <ip>77.122.5.235</ip>
  </uploader>
  <links>
    <image_link>http://img190.imageshack.us/img190/6189/samplew.mp4</image_link>
    <thumb_link>http://img190.imageshack.us/img190/6189/samplew.mp4.th.jpg</thumb_link>
    <thumb_html><a href="http://img190.imageshack.us/my.php?image=samplew.mp4" target="_blank">
        <img src="http://img190.imageshack.us/img190/6189/samplew.mp4.th.jpg" 
            alt="Free Image Hosting at www.ImageShack.us" border="0"/></a></thumb_html>
    <thumb_bb>[URL=http://img190.imageshack.us/my.php?image=samplew.mp4]
        [IMG]http://img190.imageshack.us/img190/6189/samplew.mp4.th.jpg[/IMG][/URL]</thumb_bb>
    <thumb_bb2>[url=http://img190.imageshack.us/my.php?image=samplew.mp4]
        [img=http://img190.imageshack.us/img190/6189/samplew.mp4.th.jpg][/url]</thumb_bb2>
    <video_embed><embed src="http://img190.imageshack.us/flvplayer.swf?f=Psamplew" width="480" height="338" 
        allowFullScreen="true" type="application/x-shockwave-flash"/>
</video_embed>
    <ad_link>http://img190.imageshack.us/my.php?image=samplew.mp4</ad_link>
    <done_page>http://img190.imageshack.us/content.php?page=done&l=img190/6189/samplew.mp4</done_page>
  </links>
</imginfo>
```

For example, if thumbnail image is present, **"thumb\_link"** (sub-element of **"links"**) element will contain URL of thumbnail image.<br />
<br />
In case of error the document with root element **"links"** and element **"error"** present will be returned. The **"error"** element may contain human-readable error message. <br />
<br />
Example:
```
<links>
    <error>no such file</error>
</links>
```

**Note:** this API may return HTTP redirect code which must be honored by HTTP client.