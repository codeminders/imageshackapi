# Imageshack JSON API #

## Terms ##
  * The Imageshack JSON API is free to use and subject to Imageshack's <a href='http://imageshack.us/p/rules/'>Terms of Service</a>
  * The software or web application that uses the api must already be developed or have a plan to be fully developed in near future
  * Users of said application shall be informed that Imageshack provides free image hosting
## Obtaining an API Key ##
  * To obtain an API key, please use our <a href='http://imageshack.us/p/rules/'>API Key Request form</a>.
## Making an API Call ##
  * To make an API call, make a POST request to the related endpoint accompanied by the necessary parameters ( a `*` denotes a mandatory parameter, all others are optional ) :

> ### Uploading an Image ( Basic ) ###
    * Endpoint : https://post.imageshack.us/upload_api.php
    * Parameters :
      1. `*` 	key : The api key for your application; found in email sent after filling out our <a href='http://imageshack.us/p/rules/'>API Key Request form</a>
      1. `*` 	fileupload : image file
      1. `*` format : json
      1. tags : a CSV list of tags to describe your picture
      1. public : A string setting your image to public or private where "yes" is public and "no" is private.  Images are public by default.

> ### Uploading an Image from URL ###
    * Endpoint : https://post.imageshack.us/upload_api.php
    * Parameters :
      1. `*` key : The api key for your application; found in email sent after filling out our <a href='http://imageshack.us/p/rules/'>API Key Request form</a>
      1. `*` url : The url the image is located at
      1. `*` format : json
      1. tags : a CSV list of tags to describe your picture
      1. public : A string setting your image to public or private where "yes" is public and "no" is private.  Images are public by default.

> ### Resizing an Image ###
    * Endpoint : https://post.imageshack.us/upload_api.php
    * Parameters :
      1. `*` key : The api key for your application; found in email sent after filling out our <a href='http://imageshack.us/p/rules/'>API Key Request form</a>
      1. `*` format : json
      1. `*` optimage : To resize an image, set optimage to 1
      1. `*` optsize : A string formatted in this manner, identifying the requested height and width, respectively - "[dimension1](dimension1.md)x[dimension2](dimension2.md)".  Alternatively, set "optsize=resample" to optimize your uploaded image without resizing
> > > > AND EITHER
      1. `*` fileupload : image file
> > > > OR
      1. `*` url : The url the image is located at
      1. tags : a CSV list of tags to describe your picture
      1. public : A string setting your image to public or private where "yes" is public and "no" is private.  Images are public by default.


> ### Uploading an Image into an Account ###
    * Endpoint : https://post.imageshack.us/upload_api.php
    * Parameters :
      1. `*` key : The api key for your application; found in email sent after filling out our <a href='http://imageshack.us/p/rules/'>API Key Request form</a>
      1. `*` format : json
      1. `*` fileupload : image file
> > > > OR
      1. `*` url : The url the image is located at
> > > > AND ONE OF THE FOLLOWING METHODS:
      1. `*` cookie : Registration code; found in the email sent to you after registration
> > > > OR
      1. `*` a\_username : User's Imageshack username
      1. `*` a\_password : User's Imageshack password


> ### Uploading a Video ###
    * Endpoint : https://render.imageshack.us/upload_api.php
    * Parameters :
      1. `*` key : The api key for your application; found in email sent after filling out our <a href='http://imageshack.us/p/rules/'>API Key Request form</a>
      1. `*` format : json
      1. `*` fileupload : image file
      1. frmupload : an image file to be the default frame picture for your video.  Dimensions must be the same as video to avoid screen artifacts.

> ### Return Object Structure ###
    * Example request response :

```
{
   "status":"1", //[status number of request]
   "version":8, //[Imageshack API version #]
   "timestamp":1358208945, //[Unix timestamp of API request]
   "base_url":"imageshack.us/a/", //[Base Imageshack URL of returned image]
   "id":null, //[ID of returned image, if applicable]
   "rating":{
      "ratings":0, //[number of image ratings, if applicable]
      "avg":0 //[average of all ratings ]
   },
   "files":{
      "server":"255", //[imageshack server number]
      "bucket":"9548", //[imageshack bucket number]
      "image":{
         "size":42758, //[image size in bytes]
         "content-type":"image/png", //[image MIME type ]
         "filename":"poussituxzf0.png", //[returned filename of image]
         "original_filename":"poussituxzf0.png" //[returned filename of image]
      },
      "thumb":{
         "size":6380, //[image thumb size in bytes]
         "content":"image/jpeg", //[image thumb MIME type]
         "filename":"poussituxzf0.th.png" //[image thumb filename]
      }
   },
   "resolution":{
      "width":256, //[image width]
      "height":256 //[image height]
   },
   "class":"r", //[image class, if applicable]
   "visibility":"yes", //[public or private, values are "yes" or "no"]
   "uploader":{
      "ip":"127.0.0.1" //[uploader IP, if applicable]
   },
   "links":{
      "image_link":"http://imageshack.us/a/img255/9548/poussituxzf0.png", //[direct image link]
      "image_html":"<a href='http://imageshack.us/photo/my-images/255/poussituxzf0.png/' target='_blank'><img src='http://imageshack.us/a/img255/9548/poussituxzf0.png' alt='Free Image Hosting at www.ImageShack.us' border='0'/></a>'", //[image html link]
      "image_bb":"[URL=http://imageshack.us/photo/my-images/255/poussituxzf0.png/][IMG]http://imageshack.us/a/img255/9548/poussituxzf0.png[/IMG][/URL]", //[BB image link]
      "image_bb2":"[url=http://imageshack.us/photo/my-images/255/poussituxzf0.png/][img=http://imageshack.us/a/img255/9548/poussituxzf0.png][/url]", //[BB2 image link]
      "thumb_link":"<a href='http://imageshack.us/photo/my-images/255/poussituxzf0.png/' target='_blank'><img src='http://img255.imageshack.us/img255/9548/poussituxzf0.th.png' alt='Free Image Hosting at www.ImageShack.us' border='0'/></a>'", //[thumbnail link]
      "thumb_bb":"[URL=http://imageshack.us/photo/my-images/255/poussituxzf0.png/][IMG]http://img255.imageshack.us/img255/9548/poussituxzf0.th.png[/IMG][/URL]", //[thumbnail BB link]
      "thumb_bb2":"[url=http://imageshack.us/photo/my-images/255/poussituxzf0.png/][img=http://img255.imageshack.us/img255/9548/poussituxzf0.th.png][/url]", //[thumbnail BB2 link]
      "is_link":"http://imageshack.us/photo/my-images/255/poussituxzf0.png/", //[Imageshack link]
      "done":"http://imageshack.us/content_round.php?page=done&l=img255/9548/poussituxzf0.png" //[page displaying successful upload (deprecated)]
   }
}

```


---


# XML API #

### Introduction and Usual Requirements of the XML API ###
The ImageShack Developer center allows a complete integration of ImageShack's services into any website or software via the use of an XML API, is subject to the ImageShack [Terms of Service](http://imageshack.us/p/rules/), and is **free** to use.

Terms specific to the XML API:

  * Website or software must already be developed or have a strategic plan to be developed in the near future.
  * Website or software users must be informed that ImageShack is providing free image hosting.

In order to start using your own personalized version of ImageShack's API you must first [Request a key](http://imageshack.us/api_request/). In your email, specify the number of unique visitors to your site per day and include a description of how you intend to use the ImageShack XML API.

### Unified upload API ###
ImageShack is pleased to introduce new unified API to upload/transload your images and videos

Unified API entry point is: `http://www.imageshack.us/upload_api.php` for images and `http://render.imageshack.us/upload_api.php` for video files

Supported parameters are:

  * fileupload; (input type="file") - image or video file. Mandatory unless url parameter is specified.
  * frmupload; (input type="file") - video default frame picture. Optional, used only for video upload. When you uploading your video you could supply a default frame that will be displayed when video is stopped. Dimensions of this image should be the same as video file's ones to avoid artefacts on screen.
  * url; This parameter indicates that transload method is used instead of upload
  * optsize; resize options for image in form WxH if image is uploaded/transloaded. No impact on video uploads.
  * rembar; Developer could tell to ImageShack to leave/remove information bar on thumbnail image generated by ImageShack . If you've supplied this parameter as yes or as 1 then generated thumbmail will have no information bar. No impact on video uploads
  * tags; A comma-separated list of tags to add to your video/image. E.g. family,picture. Optional
  * public; Public/private marker of your video/picture. yes means public (default), no means private. Optional
  * cookie; Registration code, optional.
  * a\_username; Username, optional.
  * a\_password; Password, optional.
  * key; Your DeveloperKey. Mandatory.

If either **cookie** or **a\_username** and **a\_password** specified, newly uploaded/transloaded video/picture will be added to the list of videos/pictures for this user.

### Resizing Images ###

The resizing of images works for both regular uploading and transloading. Send the following variables along with the variables specified above:

  * optimage = 1; (specifies that image will be resized)
  * optsize = "`[axis1]x[axis2]`"; (will resize the image to fit any intended resolution)

The following form may be useful:
```
 Resize Image? <input type="checkbox" name="optimage" id="optimage" value="1" checked onclick="optsize.disabled=!this.checked">
 <select name="optsize" id="optsize">
<option value="100x100">100x75 (avatar)</option>
<option value="150x150">150x112 (thumbnail)</option>
<option value="320x320">320x240 (for websites and email)</option>
<option value="640x640">640x480 (for message boards)</option>
<option value="800x800">800x600 (15-inch monitor)</option>
<option value="1024x1024">1024x768 (17-inch monitor)</option>
<option value="1280x1280">1280x1024 (19-inch monitor)</option>
<option value="1600x1600">1600x1200 (21-inch monitor)</option>
<option value="resample">optimize without resizing</option>
 </select>
```

### Uploading into Accounts ###

If a user specifies a valid registration code, the uploaded images will populate a user's Image Panel.

Instruct a registered and logged-in user to retrieve his or her registration code by visiting the [Registration page](http://profile.ImageShack.us/registration/). If the user has a registration cookie on his computer, the registration code can then be copied and pasted with ease.

To validate a user's registration code input, send the following variables via GET or POST to:<br /> `http://my.imageshack.us/setlogin.php`

  * login; (the registration code)
  * xml = "yes"; (specifies the return of XML)

Test the validation of a registration code:

http://imageshack.us/setlogin.php?login=badregistrationcode&xml=yes<br />
http://imageshack.us/setlogin.php?login=b2b745fce6edf3055805b07709ac34f5&xml=yes

### Starting New Slideshow with Transloaded Image ###

Submit data to the following URL `http://ImageShack.us/slideshow/index.php` using GET or POST method. Expected parameters are:

  * action=transload; (mandatory parameter and value)
  * url; (mandatory, image URL that points to JPEG/GIF/TIFF/BMP/PNG image)
  * title; (optional parameter, allows to set image title)
  * optsize; (optional, expected values are: "640x480", "320x240", "426x320". If none specified then "426x320" is assumed)

Example:

`http://ImageShack.us/slideshow/index.php?url=``http://static.flickr.com/39/84283230_4730c2ab58_b.jpg&title=snowman&action=transload`

### Starting New Slideshow with Uploaded Image ###

Submit data to the following URL `http://ImageShack.us/slideshow/index.php` using POST (multipart/form-data) method. Expected parameters are:

  * action=upload; (mandatory parameter and value)
  * fileupload; ( mandatory, image data file)
  * title; (optional parameter, allows to set image title)
  * optsize; (optional, expected values are: "640x480", "320x240", "426x320". If none specified then "426x320" is assumed)

### Starting New Slideshow with Multiple Images ###

You can build slideshow, specifying list of images either by their full URLs or by short ImageShack image IDs. All images will transloaded to ImageShack , resized to slideshow size and new slideshow will be created.

Submit data to the following URL `http://ImageShack.us/slideshow/import.php` using POST method. Expected parameters are:

  * url[.md](.md); (list of URLs. Each item can be either fully-qualified URL that points to image `[`e.g. `http://image.com/image.jpg``]` or short link to ImageShack image `[`e.g. `imgHOSTID/BUCKET/FILENAME.EXT``]`. In second case full URL will be constructed as `imgHOSTID.ImageShack.us/imgHOSTID/BUCKET/FILENAME.EXT`)
  * optsize; (optional, expected values are: "640x480", "320x240", "426x320". If none specified then "426x320" is assumed.)
  * finalize; (optional, expected values are: 'true' and 'false'. If none is specified then 'false' is assumed. This parameter control what to do when all images are uploaded. If this parameter is 'true' then user will be redirected to 'Get links' page of slideshow, otherwise user will end up in slideshow editor UI after uploading.)

Sample HTML form:
```
<form method="post" action="http://www.ImageShack.us/slideshow/import.php">
    <select name="url[]" multiple>
        <option value="http://static.flickr.com/41/84284327_88dad1fcf2_b.jpg">Picture 1, complete URL</option>
        <option value="img54/6417/piggies3at.jpg">ImageShack image link</option>
    </select>
    <input type="radio" name="finalize" value="yes">Yes
    <input type="radio" name="finalize" value="no" checked>No
    <select name="optsize">
        <option value="320x240">Small (320x240)</option>
        <option value="426x320" selected>Medium (426x320)</option>
        <option value="640x480">Big (640x480)</option>
    </select>
    <input type="submit" value="Go">
</form>
```

### Working with Galleries ###

See [Gallery API page](ImageshackGalleryAPI.md).