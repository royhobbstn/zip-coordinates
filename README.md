# zip-coordinates
Reasonable Latitude &amp; Longitude Centroid Coordinates for every 5-digit US Postal Code.  Even the ones that don't actually exist.

## What is this, really?

Say you have an application that needs the coordinates for quite a few ZipCodes.  You dig and dig and gather quite a few.  Just when you think you've got a complete set, a new data point comes in with a brand new zip.  It might even be a typo, but you have no way of knowing.
In these situations, and if your application places more of a priority on "put it on the map" rather than "this has to be perfect or I'll get sued", this is a methodology that will get you "close enough".

## How it works:

1. Start with the USA ZCTA Tiger Shapefile.  
2. Convert it to GeoJSON.
3. Create a keyed lookup of known Zips (every ZCTA the Census has data for.  Which is but a subset of all the zips you'll encounter in the wild.)
4. Create an aggregated lookup.  That is, get the average coordinates for every zip that starts with a 0, then a 1, etc.  Now get the average coordinates for every zip that starts with 00, 01, etc.  You get the picture.
5. Loop over every possible 5 digit combination.  If that number is found in the aggregated lookup, use it.  Otherwise, use the 4 digit aggregate.  If that doesn't exist, use the 3 digit aggregate, etc.

## FAQ

**Q: Aren't you creating coordinates out of thin air for thousands of ZipCodes that likely don't exist?**

*A: That's a bit harsh, but yes.*

**Q: I looked up my favorite zip and it was way off.**

*A: I believe you.  The general idea is not to be perfect.  It is to be 'close enough' for most cases.  If you want perfect you'll either have to hire a team of interns or purchase a private dataset.  Even then...*

### Prerequisities

You're going to need to have GDAL/OGR, unzip, wget, and NodeJS (10+) installed.

...Or just be lazy and download [the JSON file I checked in]().  I won't judge you either way.