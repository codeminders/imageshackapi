# Introduction #
OEMBED is an embeddable representation of media usually sent in JSON or XML format. Please see http://www.oembed.com/ for details on the standard. With an OEMBED response, a website can display an image or a video without having to deal with the media resource directly to know how to display it.

# Details #
To get an OEMBED formatted response for a media on YFrog, a consumer of the media (in this case another website embedding a photo for example) will make the following HTTP request:
```
* http://www.yfrog.com/api/oembed?url=http:\/\/yfrog.com/2pswonj (escaped version)
* http://www.yfrog.com/api/oembed?url=http%3A%2F%2Fyfrog.com%2F2pswonj (encoded version)
```

The corresponding JSON response will be:
```
{
    "version":"1.0",
    "provider_name":"yFrog",
    "provider_url":"http:\/\/yfrog.com",
    "thumbnail_url":"http:\/\/yfrog.com\/2pswonj:small",
    "width":525,
    "height":700,
    "author_url":"http:\/\/yfrog.com\/froggy.php?username=extrabaggs",
    "title":"Yfrog Image : yfrog.com\/2pswonj",
    "type":"image",
    "url":"http:\/\/img97.yfrog.com\/img97\/1103\/swon.jpg"
}
```
The consuming application or website can parse the JSON response for the appropriate element (thumbnail, URL for the image, etc.) to display on the web page.

## Support for both Photos and Videos ##
The OEMBED response works for both photos and videos uploaded on YFrog. The response for a video request will be:
```
{
    "version":"1.0",
    "provider_name":"yFrog",
    "provider_url":"http:\/\/yfrog.com",
    "thumbnail_url":"http:\/\/yfrog.com\/ehvid00001jz:small",
    "width":640,"height":360,
    "author_url":"http:\/\/yfrog.com\/froggy.php?username=sk_tester",
    "title":"Yfrog Image : yfrog.com\/ehvid00001jz",
    "type":"video",
    "html":"http:\/\/yfrog.com\/ehvid00001jz:embed"
}
```