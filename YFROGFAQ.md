# What is yfrog? #
yfrog is a service run by ImageShack that lets you share your photos on and videos on Twitter
# What's different about yfrog? #

  * It's easy to use. yfrog makes tweeting photos and videos a breeze.
  * Retweeting is even easier. Your friends will able to easily retweet any yfrog post directly from the landing page.
  * It's optimized for mobile viewing. See [example of full-screen photo view](http://img716.imageshack.us/img716/2126/tulipsr.jpg) in iPhone.
  * yfrog is supported by [ImageShack](http://imageshack.us)'s back-end for high performance and reliability.

# How do I Tweet using yfrog? #

  * From **yfrog.com**:
    1. Upload an image or video from your desktop or from an URL
    1. Enter your message
    1. Enter your credentials to Twitter
    1. Click post it
  * From your mobile device: Go to yfrog.com in your mobile browser. With iPhone, you can use our mobile-optimized interface.
  * From a yfrog hosted image: Click "(RE)Tweet this image!"
  * Use yfrog [APIs](YFrogAPI.md)
  * From mobile iPhone clients supporting yfrog (coming soon)

# Can I use yfrog URLs outside twitter? #
Yes! yfrog offers a short URL service that can be used anywhere.

# Why should developers use yfrog's APIs? #

  * yfrog has simple to use REST APIs, including one for easily [getting THUMBNAILS](YFROGthumbnails.md)
  * [ImageShack](http://imageshack.us) has been hosting images since 2004 and use of the ImageShack back-end ensures high performance and reliability for yfrog
  * We support HTTPs to protect user Twitter credentials from been snooped in-transit

# Are the yfrog APIs free for developers? #
Yes! But you need a DeveloperKey.

# How can I keep updated about yfrog new features and APIs? #
Just follow [@yfrog](http://twitter.com/yfrog) on twitter
What file types does yfrog support?

Photo

  * jpeg
  * png
  * bmp
  * gif

Video

  * flv
  * mpeg
  * mkv
  * wmv
  * mov
  * 3gp
  * mp4
  * avi
  * Many others


Please let us know if there is a file type you would like us to support. Send us a message on Twitter @yfrog.

# How do I get “`from [MyApp]`” appended to updates sent from my API application? #

Due to Twitter API changes, only applications posting directly and using OAuth can submit "source" parameter [(Twitter FAQ reference)](http://apiwiki.twitter.com/FAQ#HowdoIget“fromMyApp”appendedtoupdatessentfrommyAPIapplication).
This still works for old applications, which have been registered before OAuth was introduced at Twitter. So if your application is one of such applications, you can specify your app name via _'source'_ parameter. If not, unfortunately nothing could be done about it.