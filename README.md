# cities

This is a collection of `.poly` files for cities, with the definition of 'city' being the area one level under the region/state level. There isn't a whole lot of concern here for discrepancies between cities, towns, villages, etc.

These `.poly` files are used to then extract just the city's OSM file from a greater region's OSM file. For example, creating an exact OSM file for Boston from the North America OSM file. More information on actually using the `.poly` files is provided at the bottom of this document.

The ultimate goal is to have them all, but it's a rough process right now. The process explained below shows how to retrieve the `.poly` file for a specific city, but the process I've gone through to gather most of the files in this repository is much more automated and uses [Overpass Turbo](http://overpass-turbo.eu/).

### How To Get The Poly File For A Specific City

Sometimes a city won't have a Relation ID, or the Relation that exists will be broken. For those instances, the final OSM file can be created manually by tracing the city at [http://extract.bbbike.org/](http://extract.bbbike.org/). Just make sure to select one of the 'OSM XML' formats in the top pulldown menu there.

* Go to [http://nominatim.openstreetmap.org/](http://nominatim.openstreetmap.org/) and search for the city you'd like added

    ![](images/howto1.png)

* Click the 'details' link for that city in the left column

    ![](images/howto2.png)

* Make sure that the map on the right displays the full city border

    ![](images/howto3.png)

* Copy the number for 'OSM: relation'

    ![](images/howto4.png)

* Go to [http://polygons.openstreetmap.fr/](http://polygons.openstreetmap.fr/), paste the number into the form, and click the Submit button

    ![](images/howto5.png)

* Click the 'poly' link to open the file in the browser, then use `File -> Save As` to save the file

    ![](images/howto6.png)

* The naming convention I've been using is `city-name_state-abbreviation.poly`. For example, `holyoke_ma.poly`

### How To Use The Poly File

You can use the `.poly` file to extract that region from a greater region's OSM file.

* Install [Osmosis](http://wiki.openstreetmap.org/wiki/Osmosis)
    * If you're on a Mac, I suggest you use [Homebrew](http://mxcl.github.io/homebrew/) to install it with `brew intsall osmosis`
* Download the `.osm.pbf` file for the region that the city is in from [http://download.geofabrik.de/](http://download.geofabrik.de/)
* Run this to extract the city's OSM file out of the greater region's OSM file:
`osmosis --read-pbf-fast file="YOUR-REGION-latest.osm.pbf" --bounding-polygon file="CITY-NAME_STATE.poly" --write-xml file="CITY-NAME_STATE.osm"`
For example:
`osmosis --read-pbf-fast file="north-america-latest.osm.pbf" --bounding-polygon file="holyoke_ma.poly" --write-xml file="holyoke_ma.osm"`
