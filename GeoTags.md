# Introduction #

When posting media to ImageShack or Yfrog you can specify location information. This
location will be stored along with them image and could be used to show location where
it was taken.

## Details ##

Location information is presented in form of tags. This practice also often referred to as  ["geotagging"](http://en.wikipedia.org/wiki/Geotagging).

3 tags needs to be specified. Example:

```
geotagged
geo:lat=57.64911
geo:lon=10.40744
```

This describes the geographic coordinates of a particular location in terms of latitude (geo:lat) and longitude (geo:lon). These are expressed in decimal degrees in the [WGS84](http://en.wikipedia.org/wiki/WGS84) datum.

## 3rd party sites ##

When image is posted to Twitter using [Yfrog APIs](YFrogAPI.md), location information will be automatically submitted to Twitter.

## References ##
  1. [Wikipedia: Geotagging](http://en.wikipedia.org/wiki/Geotagging)
  1. [Wikipedia: Geotagging in tag-based systems](http://en.wikipedia.org/wiki/Geotagging#Geotagging_in_tag-based_systems)