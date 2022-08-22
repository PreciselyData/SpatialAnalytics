# Spatial Utilities

Latest version of the Spatial Utilities can be downloaded from the [release](https://github.com/PreciselyData/SpatialAnalytics/releases) section of the github repository


## Utilities

### Tile Generator
The Tile Generator is a command-line utility, named cache_builder.bat on Windows and cache_builder.sh on Linux, that generates MapTiling requests to send to a MapTiling service or to save to a file. Saving a request to a file is useful for seeding the tile cache in batch or for generating tiles offline.

### WMTS Tile Generator
OGC-compliant Web Map Tile Service (WMTS) built to the OGC specifications for WMTS versions 1.0.0 (located at http://www.opengeospatial.org/standards/wmts).

The WMTS Tile Generator is a command-line utility, named tile_builder.bat on Windows and tile_builder.sh on Linux, that executes batch runs to generate map tiles for the WMTS service and optionally seed the WMTS tile cache.

### Map Uploader
Map Uploader is a tool that copies the properties of the layers in a MapInfo Pro map to a Spectrum Spatial server. It takes the information of one map stored in MapInfo Pro and stores the equivalent information in a set of named resources on the server.

### CLI

Administration utility for managing Spatial Analytics server