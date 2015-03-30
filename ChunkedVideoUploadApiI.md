# Chunked Upload API #
## Summary ##
In order to upload big video or image files with ability to suspend transfers and survive network errors we are introducing chunked upload API.<br>
The API using standard HTTP protocol and should work with most HTTP stack libraries. With this API user have flexibility of either upload whole media file as one HTTP request, or using multiple HTTP requests. If some of upload requests failed, partial data is saved, and upload could be resumed from last saved position.<br>
<br>
<h2>API methods</h2>
Chunked upload API provides 3 methods:<br>
<br>
<ul><li>start: Initiate upload, passing file metadata like tags, user information (but not actual file content)<br>
</li><li>put: Upload actual data. Data could be uploaded starting from certain position.<br>
</li><li>getlength: Allows to get uploaded data size.</li></ul>


<h2>Upload Process</h2>
<ol><li>Pass metadata information to server, retrieve upload URL (start method, POST)<br>
</li><li>Upload File data in chunks using put (PUT) method. If the upload was interrupted by network error you can use getlength (GET) method to find out how much data have been saved on server and resume from this point.</li></ol>

<h3>Initiating Upload</h3>
Each upload should start with POST call to<br>
URL: <a href='http://render.imageshack.us/renderapi/start'>http://render.imageshack.us/renderapi/start</a><br>
Content-type: multipart/form-data<br>
Method: POST<br>
<br>
Parameters:<br>
<br>
<i>filename</i> - name of file to be uploaded, optional. Used to determine target file name, if not specified, media file.....mp4 will be used as destination file name<br>
<i>key</i> - your ImageShack API developer key<br>
<i>cookie</i> - user's cookies, optional. If specified, media file will be linked to user's account<br>
<i>tags</i> - comma-separated list of tags, optional. Could also include <a href='GeoTags.md'>geo tags</a><br>
<i>public</i> - yes/no, optional. if specified, media file visibility will be set to specified value; otherwise default user visibility <i>settings</i> (if cookies or username/password are specified) will be used<br>
<i>a_username</i> - Imageshack user's name, optional<br>
<i>a_password</i> - Imageshack user's password, optional<br>
<i>t_username</i> - Twitter user's name, optional<br>
<i>t_password</i> - Twitter user's password, optional<br>
<i>t_verify_url</i> - Signed URL that points to Twitter's verify_credentials.xml<br>
<i>content_type</i> – content type of uploaded file, optional. If not specified then we are trying to guess content type based on file extension. If content_type is identified as one of :<br>
<ul><li>image/jpeg<br>
</li><li>image/png<br>
</li><li>image/gif<br>
</li><li>image/bmp<br>
</li><li>image/tiff<br>
</li><li>application/pdf<br>
then file will be uploaded and proceed as image; otherwise file will be treated as video file.</li></ul>


<br>
The server will respond with XML document.<br>
<br>
Sample server response text:<br>
<pre><code>&lt;?xml version="1.0" encoding="UTF-8"?&gt;<br>
&lt;uploadInfo<br>
    link="http://yfrog.us/65huxz"<br>
    putURL ="http://img676.imageshack.us/renderapi/put/b21765e5"<br>
    getlengthURL ="http://img676.imageshack.us/renderapi/getlength/b21765e5"<br>
/&gt;<br>
</code></pre>
where:<br>
<i>putURL</i> - URL which should be used to upload file data<br>
<i>getlengthURL</i> - URL which should be used to query current file size<br>
<i>link</i> - link to uploaded file page (HTML) hosted at imageshack<br>

<h4>How authentication with Twitter credentials work</h4>

If you've supplied <i>t_username</i> and <i>t_password</i> then we are trying to contact Twitter in order to check your credentials. If check was successful then we'll continue with file upload, media file will be visible in list of your images on <a href='http://yfrog.com/froggy.php'>http://yfrog.com/froggy.php</a>

If you've supplied <i>t_username</i> and <i>t_verify_url</i> then we'll check if information retuned by Twitter using signed URL matches the expected one. If check was successful then we'll continue with file upload, media file will be visible in list of your images on <a href='http://yfrog.com/froggy.php'>http://yfrog.com/froggy.php</a>

If authentication on Twitter was failed, a 401 HTTP error is returned back<br>
<br>
<br>
<h3>Uploading Data</h3>
Each time you need to upload block of file you should perform a PUT call to putURL (as retrieved on previous stage).<br>
The URL may contain query string!<br>
<br>
URL: (returned in putURL attribute of uploadInfo response to start method)<br>
Method: PUT<br>
<br>
When uploading partial content, use HTTP 1.1 Content-Range headers.<br>
Headers example:<br>
<pre><code>Content-Length: 203873<br>
Content-Range: bytes 0-256/203873<br>
</code></pre>

In this example we are sending first 257 bytes of file which total length is 203873.<br>
<br>
After completion of block server should return HTTP status "202 Accepted". After last block, "201 Created" will be returned.<br>
<br>
Sample server 201 response text for image:<br>
<pre><code>&lt;?xml version="1.0" encoding="iso-8859-1"?&gt;&lt;imginfo xmlns="http://ns.imageshack.us/imginfo/7/" version="7" timestamp="1266245431"&gt;<br>
  &lt;rating&gt;<br>
    &lt;ratings&gt;0&lt;/ratings&gt;<br>
    &lt;avg&gt;0.0&lt;/avg&gt;<br>
  &lt;/rating&gt;<br>
  &lt;files server="714" bucket="6510"&gt;<br>
     &lt;image size="122" content-type="image/gif"&gt;imageaz.gif&lt;/image&gt;<br>
  &lt;/files&gt;<br>
  &lt;resolution&gt;<br>
    &lt;width&gt;12&lt;/width&gt;<br>
    &lt;height&gt;21&lt;/height&gt;<br>
  &lt;/resolution&gt;<br>
  &lt;class&gt;r&lt;/class&gt;<br>
  &lt;visibility&gt;yes&lt;/visibility&gt;<br>
  &lt;uploader&gt;<br>
    &lt;ip&gt;99.132.34.183&lt;/ip&gt;<br>
    &lt;cookie&gt;444445415b312c66ae0b4c9fe6dc47f2&lt;/cookie&gt;<br>
  &lt;/uploader&gt;<br>
  &lt;links&gt;<br>
    &lt;image_link&gt;http://img714.imageshack.us/img714/6510/imageaz.gif&lt;/image_link&gt;<br>
    &lt;image_html&gt;&amp;lt;a href=&amp;quot;http://img714.imageshack.us/my.php?image=imageaz.gif&amp;quot; target=&amp;quot;_blank&amp;quot;&amp;gt;&amp;lt;img src=&amp;quot;http://img714.imageshack.us/img714/6510/imageaz.gif&amp;quot; alt=&amp;quot;Free Image Hosting at www.ImageShack.us&amp;quot; border=&amp;quot;0&amp;quot;/&amp;gt;&amp;lt;/a&amp;gt;&lt;/image_html&gt;<br>
    &lt;image_bb&gt;[URL=http://img714.imageshack.us/my.php?image=imageaz.gif][IMG]http://img714.imageshack.us/img714/6510/imageaz.gif[/IMG][/URL]&lt;/image_bb&gt;<br>
    &lt;image_bb2&gt;[url=http://img714.imageshack.us/my.php?image=imageaz.gif][img=http://img714.imageshack.us/img714/6510/imageaz.gif][/url]&lt;/image_bb2&gt;<br>
    &lt;thumb_html&gt;&amp;lt;a href=&amp;quot;http://img714.imageshack.us/my.php?image=imageaz.gif&amp;quot; target=&amp;quot;_blank&amp;quot;&amp;gt;&amp;lt;img src=&amp;quot;http://www.imageshack.us/thumbnail.png&amp;quot; alt=&amp;quot;Free Image Hosting at www.ImageShack.us&amp;quot; border=&amp;quot;0&amp;quot;/&amp;gt;&amp;lt;/a&amp;gt;&lt;/thumb_html&gt;<br>
    &lt;thumb_bb&gt;[URL=http://img714.imageshack.us/my.php?image=imageaz.gif][IMG]http://www.imageshack.us/thumbnail.png[/IMG][/URL]&lt;/thumb_bb&gt;<br>
    &lt;thumb_bb2&gt;[url=http://img714.imageshack.us/my.php?image=imageaz.gif][img=http://www.imageshack.us/thumbnail.png][/url]&lt;/thumb_bb2&gt;<br>
    &lt;yfrog_link&gt;http://yfrog.com/juimageazg&lt;/yfrog_link&gt;<br>
    &lt;yfrog_thumb&gt;http://yfrog.com/juimageazg.th.jpg&lt;/yfrog_thumb&gt;<br>
    &lt;ad_link&gt;http://img714.imageshack.us/my.php?image=imageaz.gif&lt;/ad_link&gt;<br>
    &lt;done_page&gt;http://img714.imageshack.us/content.php?page=done&amp;amp;l=img714/6510/imageaz.gif&lt;/done_page&gt;<br>
  &lt;/links&gt;<br>
&lt;/imginfo&gt;<br>
<br>
</code></pre>

Sample server 201 response text for video:<br>
<pre><code>&lt;imginfo xmlns="http://ns.imageshack.us/imginfo/7/" version="7" timestamp="1253212661"&gt;<br>
  &lt;rating&gt;<br>
    &lt;ratings&gt;0&lt;/ratings&gt;<br>
    &lt;avg&gt;0.0&lt;/avg&gt;<br>
  &lt;/rating&gt;<br>
  &lt;files server="11" bucket="8175"&gt;<br>
     &lt;image size="0" content-type="video/mp4"&gt;samplep.mp4&lt;/image&gt;<br>
  &lt;/files&gt;<br>
  &lt;resolution&gt;<br>
    &lt;width&gt;0&lt;/width&gt;<br>
    &lt;height&gt;0&lt;/height&gt;<br>
  &lt;/resolution&gt;<br>
  &lt;video-info&gt;<br>
    &lt;status&gt;queued&lt;/status&gt;<br>
    &lt;duration&gt;0&lt;/duration&gt;<br>
  &lt;/video-info&gt;<br>
  &lt;class&gt;r&lt;/class&gt;<br>
  &lt;visibility&gt;yes&lt;/visibility&gt;<br>
  &lt;uploader&gt;<br>
    &lt;ip&gt;99.132.34.183&lt;/ip&gt;<br>
    &lt;cookie&gt;444445415b312c66ae0b4c9fe6dc47f2&lt;/cookie&gt;<br>
  &lt;/uploader&gt;<br>
  &lt;links&gt;<br>
    &lt;image_link&gt;http://img11.imageshack.us/img11/8175/samplep.mp4&lt;/image_link&gt;<br>
    &lt;thumb_html&gt;&amp;lt;a href=&amp;quot;http://img11.imageshack.us/my.php?image=samplep.mp4&amp;quot; target=&amp;quot;_blank&amp;quot;&amp;gt;&amp;lt;img src=&amp;quot;http://img11.imageshack.us/img11/8175/samplep.mp4.th.jpg&amp;quot; alt=&amp;quot;Free Image Hosting at www.ImageShack.us&amp;quot; border=&amp;quot;0&amp;quot;/&amp;gt;&amp;lt;/a&amp;gt;&lt;/thumb_html&gt;<br>
    &lt;thumb_bb&gt;[URL=http://img11.imageshack.us/my.php?image=samplep.mp4][IMG]http://img11.imageshack.us/img11/8175/samplep.mp4.th.jpg[/IMG][/URL]&lt;/thumb_bb&gt;<br>
    &lt;thumb_bb2&gt;[url=http://img11.imageshack.us/my.php?image=samplep.mp4][img=http://img11.imageshack.us/img11/8175/samplep.mp4.th.jpg][/url]&lt;/thumb_bb2&gt;<br>
    &lt;yfrog_link&gt;http://yfrog.us/0bsamplepz&lt;/yfrog_link&gt;<br>
    &lt;yfrog_thumb&gt;http://yfrog.us/0bsamplepz.th.jpg&lt;/yfrog_thumb&gt;<br>
    &lt;frame_link&gt;http://img11.imageshack.us/img11/8175/samplep.mp4.frm.jpg&lt;/frame_link&gt;<br>
    &lt;frame_html&gt;&amp;lt;a href=&amp;quot;http://img11.imageshack.us/my.php?image=samplep.mp4&amp;quot; target=&amp;quot;_blank&amp;quot;&amp;gt;&amp;lt;img src=&amp;quot;http://img11.imageshack.us/img11/8175/samplep.mp4.frm.jpg&amp;quot; alt=&amp;quot;Free Image Hosting at www.ImageShack.us&amp;quot; border=&amp;quot;0&amp;quot;/&amp;gt;&amp;lt;/a&amp;gt;&lt;/frame_html&gt;<br>
    &lt;frame_bb&gt;[URL=http://img11.imageshack.us/my.php?image=samplep.mp4][IMG]http://img11.imageshack.us/img11/8175/samplep.mp4.frm.jpg[/IMG][/URL]&lt;/frame_bb&gt;<br>
    &lt;frame_bb2&gt;[url=http://img11.imageshack.us/my.php?image=samplep.mp4][img=http://img11.imageshack.us/img11/8175/samplep.mp4.frm.jpg][/url]&lt;/frame_bb2&gt;<br>
    &lt;video_embed&gt;&amp;lt;embed src=&amp;quot;http://img11.imageshack.us/flvplayer.swf?f=Msamplep&amp;quot; width=&amp;quot;640&amp;quot; height=&amp;quot;380&amp;quot; allowFullScreen=&amp;quot;true&amp;quot; wmode=&amp;quot;transparent&amp;quot; type=&amp;quot;application/x-shockwave-flash&amp;quot;/&amp;gt;<br>
&lt;/video_embed&gt;<br>
    &lt;ad_link&gt;http://img11.imageshack.us/my.php?image=samplep.mp4&lt;/ad_link&gt;<br>
    &lt;done_page&gt;http://img11.imageshack.us/content.php?page=done&amp;amp;l=img11/8175/samplep.mp4&lt;/done_page&gt;<br>
  &lt;/links&gt;<br>
&lt;/imginfo&gt;<br>
</code></pre>

<h3>Retrieving Size of Partially Uploaded File</h3>

URL: (returned in getlengthURL attribute of uploadInfo response to start method)<br>
Method: GET<br>
<br>
The size of the content will be returned in response body.<br>
<br>


<h3>If your upload fails:</h3>

Server will return xml:<br>
<pre><code>&lt;error code="CODE"&gt;MESSAGE&lt;/error&gt;<br>
</code></pre>

Currently only not_found error code is supported.<br>
<br>
Possible HTTP error codes:<br>
404 Not Found - URL you are requesting is not found or command is not recognized<br>
405 Method Not Allowed - Method you are calling is not supported<br>
400 Bad Request - Your request is bad formed, for example: missing or wrong UUID, invalid content-length.<br>
403 Forbidden - Wrong developer key<br>