# ImageShack Gallery API #

API endpoint URL is: http://www.imageshack.us/gallery_api.php

**Supported parameters are:**
  * image (array or string);  image list (or single image in imageshack-url format) for create gallery, that always uploaded on imageshack. image url example: img123/4567/filename.ext <br />**for action 'create':** parameter 'image" can contain image width, image height and thumbnail flag ('y' or 'n'), delimited by ';'.<br />**example:** image=img123/4567/filename.ext;640;480;y<br />**important:** now you can add your personal images only
  * g (string); existing gallery name. used for edit, delete, view gallery and for adding image(s) to existing gallery
  * action (string); gallery action, values: create, edit, add, delete, view (default, if "action" not specified)
  * title (string); gallery title, optional
  * cookie (string); users cookie
  * token (string); identification of anonymous users;
  * name (string); used for set wanted file name of the gallery file. if a desired gallery name is already in use, then random symbols will be added to this name until a unique name is generated. If gallery name was not sent – API-script will make gallery name based on the name of first uploaded file
  * user (string); username of registered ImageShack user
  * start (int); used for action ‘gallery\_list’, indicate number of album from which it is needed to begin a selection; default - 0
  * limit (int); used for action ‘gallery\_list’, indicate albums count in the selection; default – 20, max - 100


for identification gallery owner used 'cookie' (for logged in user) or token (for anonymous)
Please note that cookie have a precendence.

**cookie:**
cookie identifies already registered ImageShack user. All galleries made by user with the same cookies are linked to this user and available in ‘my albums’ page.

**token description:**
if user have no cookies (not an ImageShack’s registered user), he can use a token then. A token is a unique hash that makes a link between gallery creator and gallery.

User can edit or delete any gallery that have the token he sent.
User cannot add image, delete image or change gallery if he does not know gallery token.

**How tokens work?**

During creation of gallery API checks for ‘cookie’ and ‘token’ parameters passed by user. If there are none, API generates unique token string, stores it in gallery and passes it back to user in XML response.
For each next file to be added into the gallery you must supply gallery token, otherwise you have no rights to change gallery content.

You can pass the same token for every gallery you making, then you’ll be able to manage all galleries made with your software.

Please note that token does not allow to query all albums made with given token. In order to manage list of personal galleries user should be logged.


**unique gallery  identifier**
unique gallery identifier it is pair of gallery server and gallery name. for example: img123 and my\_gallery

**available HTTP request type**
you can use either of GET or POST HTTP request


**actions description**

**create**
create gallery from given list of images;  assign optional title to gallery

_parameters:_
  * image
  * title (optional)
  * cookie or token
  * name (optional)
_response:_
_on success:_ (the same XML returned also for **edit**, **add** and **delete\_image**)
```
<gallery version="2" updated="1254914155">
    <server>123</server>
    <name>my_gallery</name>
    <title/>
    <uploader>
        <username/>
        <token>ksdfas654kljfnsd89745kldsfg</token>
    </uploader>
    <files total="2">
        <file>
            <server>123</server>
            <name>image1.jpg</name>
            <bucket>4567</bucket>
            <thumbnail>true</thumbnail>
            <width>928</width>
            <height>792</height>
        </file>
        <file>
            <server>234</server>
            <name>image2.jpg</name>
            <bucket>5678</bucket>
            <thumbnail>true</thumbnail>
            <width>928</width>
            <height>792</height>
        </file>
    </files>
    <links>
        <gallery_url>http://img123.imageshack.us/gal.php?g=my_gallery</gallery_url>
        <player_url>http://img123.imageshack.us/slideshow/webplayer.php?g=my_gallery</player_url>
        <yfrog_url>http://yfrog.com/my_galleryx</yfrog_url>
        <embed_code>
            <embed src="http://img123.imageshack.us/slideshow/smilplayer.swf" width="320" 
             height="240"name="smilplayer" id="smilplayer" bgcolor="#ffffff" menu="false" 
             type="application/x-shockwave-flash"
             pluginspage=http://www.macromedia.com/go/getflashplayer
             flashvars="id=img123/my_gallery"/>
        </embed_code>
    </links>
</gallery>
```
_on fail:_
```
<?xml version="1.0"?>
<errors>
    <error code="io_error">Unable to save album information</error>
</errors>
```

_available errors codes:_
|**code**|**text**|
|:-------|:-------|
|io\_create\_error|Unable to create new album file|
|io\_read\_error|Unable to read album information|
|io\_save\_error|Unable to save album information|
|bad\_parameter\_file|Invalid file name `<filename>`|
_request example:_
```
http://www.imageshack.us/gallery_api.php?action=create&image[]=img123/4567/image1.jpg&image[]=img234/5678/image2.jpg&name=my_gallery&token=ksdfas654kljfnsd89745kldsfg
```

**edit**
edit gallery 'g': change 'image' list, title 'title'
existing gallery file overwriting.
_parameters:_
  * g
  * cookie or token
  * image
  * title (optional)
_response:_
_on success:_ see XML in **create** description
_on fail:_ see XML structure in **create** description

_available errors code:_
|**code**|**text**|
|:-------|:-------|
|authentication\_failed\_save\_album|You should be logged in to save album|
|io\_exists\_error|Album does not exist or not readable|
|not\_owner\_save\_album|You are not authorized to modify specified album|
|io\_read\_error|Unable to read album information|
|io\_save\_error|Unable to save album information|
|bad\_parameter\_file|Invalid file name `<filename>`|

_request example:_
```
http://img123.imageshack.us/gallery_api.php?action=edit&title=my%20new%20title&image=img123/4567/somefile.jpg&g=my_gallery
```

**add**
add files 'image' to gallery 'g'
_parameters:_
  * g
  * cookie or token
  * image
_response:_
_on success:_ see XML in **create** description
_on fail:_ see XML structure in **create** description

_available errors code:_
|**code**|**text**|
|:-------|:-------|
|authentication\_failed\_add\_image|You should be logged in to save album|
|io\_exist\_error|Album does not exist or not readable|
|not\_owner\_add\_image|You are not authorized to modify specified album|
|io\_read\_error|Unable to read album information|
|bad\_parameter\_file|Invalid file name `<filename>`|

_request examples:_
```
http://img123.imageshack.us.gallery_api.php?action=add&image[]=img345/6789/newfile.jpg&image[]=img3/789/newfile2.jpg&g=my_gallery
```

**delete**
delete gallery 'g'
_parameters:_
  * g
  * cookie or token
_response:_
_on success:_
```
<?xml version="1.0" ?>
<gallery version="1.0" />
```
_on fail:_ see XML structure in **create** description

_available errors code:_
|**code**|**text**|
|:-------|:-------|
|authentication\_failed\_delete|You should be logged in to delete album|
|io\_exist\_error|Album does not exist or not readable|
|not\_owner\_delete|You are not authorized to delete specified album|
|db\_delete\_error|We were unable to delete album|
|io\_delete\_error|We were unable to delete album|


_request example:_
```
http://img123.imageshack.us.gallery_api.php?action=delete&g=my_gallery
```

**delete\_image**    **important:** now it works only for registered users

remove image 'image' from gallery 'g'
parameters:
  * g
  * cookie
  * image

_response:_
on success: see XML in create description
on fail: see XML structure in create description

_available errors code:_
|code|text|
|:---|:---|
|authentication\_failed\_delete\_image|You should be logged in or have token to delete image from album|
|no\_image|No image specified for deletion from an album|
|io\_exist\_error|Album does not exist or not readable|
|not\_owner\_delete\_image|You are not authorized to delete specified image from album|
|io\_read\_error|Unable to read album information|
|io\_save\_error|Unable to save album information|


_request example:_
```
http://img123.imageshack.us/gallery_api.php?action=delete_image&g=my_gallery&image=img123/4567/someimage.jpg
```


**view**
get data of gallery 'g'
_parameters:_
  * g
_response:_
_on success:_ see XML in **create** description
_on fail:_ see XML structure in **create** description

_available errors code:_
|**code**|**text**|
|:-------|:-------|
|not\_exist|Specified album does not exist|


_request example:_
```
http://img123.imageshack.us.gallery_api.php?g=my_gallery&view=xml
```

**gallery\_list**
get users gallery list

parameters:
  * user
  * start (optional)
  * limit (optional)

_response:_
on success:
```
<galleries version="2">
    <count>
        <total>20</total>
        <batch>2</batch>
    </count>
    <gallery added="1254156539">
        <server>123</server>
        <name>my_gallery</name>
        <title/>
        <links>
            <gallery_url>
                http://img123.imageshack.us/gal.php?g=my_gallery
            </gallery_url>
            <player_url>
                http://img123.imageshack.us/slideshow/webplayer.php?id=my_gallery
            </player_url>
            <yfrog_url>
                http://yfrog.com/my_galleryx
            </yfrog_url>
            <embed_code>
                <embed src="http://img123.imageshack.us/slideshow/smilplayer.swf"
                    width="320" height="240" name="smilplayer" id="smilplayer" 
                    bgcolor="#ffffff" menu="false" type="application/x-shockwave-flash" 
                    pluginspage="http://www.macromedia.com/go/getflashplayer" 
                    flashvars="id=img123/my_gallery"/>
            </embed_code>
        </links>
    </gallery>
    <gallery added="1254156508">
        <server>234</server>
        <name>image.jpg</name>
        <title/>
        <links>
            <gallery_url>
                http://img234.imageshack.us/gal.php?g=image.jpg
            </gallery_url>
            <player_url>
                http://img234.imageshack.us/slideshow/webplayer.php?id=image.jpg
            </player_url>
            <yfrog_url>
                http://yfrog.com/imagejx
            </yfrog_url>
            <embed_code>
                <embed src="http://img234.imageshack.us/slideshow/smilplayer.swf"
                    width="320" height="240" name="smilplayer" id="smilplayer" 
                    bgcolor="#ffffff" menu="false" type="application/x-shockwave-flash" 
                    pluginspage="http://www.macromedia.com/go/getflashplayer" 
                    flashvars="id=img234/image.jpg"/>
            </embed_code>
        </links>
    </gallery>
</galleries>
```

on fail:
see XML structure in create description


_available errors code:_
|code|text|
|:---|:---|
|db\_error\_album\_list|We were unable to fetch list of albums|
|no\_gallery|Specified user have no albums|

_request example:_
```
http://www.imageshack.us/gallery_api.php?action=gallery_list&user=username&start=5&limit=10
```