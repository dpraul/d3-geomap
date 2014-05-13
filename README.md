# d3-geomap

`d3.geomap` is designed to become a
[reusable](http://bost.ocks.org/mike/chart/) geographic map for D3.

It is in early development, currently consisting of a plain map `d3.geomap()`
and choropleth map `d3.geomap.choropleth()`. See a [demo choropleth map](http://maps.ramiro.org/global-slavery-index/)
created with d3.geomap.

## d3.geomap

### Usage

    var worldmap = d3.geomap()
        .geofile('/data/worldcountries.topojson');

    d3.select("#map")
        .call(worldmap.draw, worldmap);


## d3.geomap.choropleth

### Usage

    var worldmap = d3.geomap.choropleth()
        .geofile('/data/worldcountries.topojson')
        .width(1200)
        .height(780)
        .column('Calculated Percentage');

    d3.csv('data.csv', function(error, data) {
        d3.select("#map")
            .datum(data)
            .call(worldmap.draw, worldmap);
    });

### Data format

A list of objects that have an iso3 and at least one other property. The property
to be used to colorize the choropleth map is set in the `colum()` method.

    [
        {iso3: 'ESP', column1: 'value1', column2: 'value2'},
        {iso3: 'FRA', column1: 'value1', column2: 'value2'}
    ]

## Installing from source

    $ git clone https://github.com/yaph/d3-geomap.git
    $ cd d3.geomap
    $ npm install

Start the development server

    $ npm install

Open `http://localhost:8000/examples/` in a browser and choose to view one of
the example maps.

## Creating a topojson file

First download a shapefile with administrative boundaries from [naturalearthdata.com](http//www.naturalearthdata.com/).

    wget http://www.naturalearthdata.com/http//www.naturalearthdata.com/download/10m/cultural/ne_10m_admin_0_countries.zip

Convert the shapefile to GeoJSON.

    ogr2ogr -f GeoJSON units.json ne_10m_admin_0_countries.shp

Convert GeoJSON to Topojson using simplification to reduce file size. The SU_A3
(ISO3 country code) is used as the ID and the name as a property.

    ../node_modules/topojson/bin/topojson --simplify-proportion .08 --id-property SU_A3 -p name=NAME -o worldcountries.topojson  units.json

## References

* [bl.ocks.org Natural Earth](http://bl.ocks.org/mbostock/4479477)
* [bl.ocks.org click-to-zoom via transform](http://bl.ocks.org/mbostock/2206590)