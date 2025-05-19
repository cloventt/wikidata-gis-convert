# Wikidata GIS tools
This is some scripts I bashed together to convert GIS data into a format that can be easily imported to Wikidata.

The intended workflow is something like this:

1. Use this tool to pull data from an ArcGIS Feature Server and coerce to a CSV document
2. Import the CSV to OpenRefine and work with it in there

The major issue is that GIS data typically represents polygons showing the perimeter of some point of interest.
However, Wikidata uses the P625 `coordinate location` property, which is a single point. This script processes the
polygons to compute a "point of isolation", which _usually_ is a good approximation of the visual centre of a polygon.

Further, it will then query the OpenStreetMap Overpass API to detect if that point is contained within any ways on the
map. It can then optimistically grab the Way IDs of those objects, essentially reconciling against the OpenStreetMap 
data.

## Usage
You should install `poetry` on your machine. Poetry allows you to manage dependencies and virtual environments in a
way that keeps your system tidy. Go to [python-poetry.org](https://python-poetry.org/) for installation instructions.

You will also need a version of Python between 3.9 and 3.12. I recommend using `pyenv` to manage multiple installations
of Python if you need that.

To get set up run this in your terminal:
```commandline
git clone https://github.com/cloventt/wikidata-gis-tools.git
cd wikidata-gis-tools
poetry install
```

If all that works you can the run:
```commandline
poetry run jupyter notebook
```

This will start up the notebook server and open it in your web browser.