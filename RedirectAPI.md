# Redirect API #

# Introduction #

We are annoncing new type of API - redirect API, that allows to integrate your website with `ImageShack` by placing a special form that will upload images to `ImageShack` and pass the results to your scripts.

# Details #

Endpoint URL for redirect API is http://imageshack.us/redirect_api.php for image uploads/transloads and http://render.imageshack.us/redirect_api.php for video uploads/transloads.
Only POST HTTP requests are accepted. For uploads form should have enctype set to **multipart/form-data**

# Parameters #

Redirect API uses the same parameters as [ImageshackAPI](ImageshackAPI.md).
**The `ImageShack` developer key parameter (key) is mandatory**
Plus, there are some specific parameters:

  * success\_url - URL to redirect in case of success. This URL can include following placeholders:
    * %u Uploaded picture/video URL (link to `ImageShack` page)
    * %y Uploaded picture/video URL (link to yfrog.com page)
    * %s `ImageShack` server
    * %b `ImageShack` bucket
    * %i `ImageShack` filename

Example:
```
http://bit.ly?url=%y
```
will be substituted with something like:
```
http://bit.ly/?url=http://yfrog.com/fbtwitterlogowp
```

  * error\_url - URL to redirect in case of error. This URL automatically receives two GET parameters
    * error - error code
    * message - human-readable error message string


# Sample form #

```
<form method="post" enctype="multipart/form-data" action="http://imageshack.us/redirect_api.php">
    <input type="file" name="media"/>
    <input type="hidden" name="key" value="YOUR_DEVELOPER_KEY_HERE">
    <input type="hidden" name="error_url" value="http://localhost/error.php">
    <input type="hidden" name="success_url" value="http://bit.ly?url=%y">
    <input type="submit"/>
</form>
```