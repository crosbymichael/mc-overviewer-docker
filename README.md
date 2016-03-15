# Minecraft Overviewer

Generate a Google Maps like map of your minecraft world.  Documentation for overview can be
found [here](http://overviewer.org/).


## Usage

This Dockerfile requires two volumes owned by UID:GID 1 ( default ).  One volume must be mounted 
under `/minecraft` which contains a world directory for the world that you wish to create a
map of.  The other is the output directory that will contain the generated map mounted under
`/mcmap`.

You will need a config file in the minecraft server root named `overviewer.cfg` where you can specify
any processing options. The config file should have at least 2 lines defining the worlds directory
as well as the output directory. An example overviewer.cfg is:

```
worlds["survival"] = "/minecraft/world"
outputdir = "/mcmap"
```

In addition to the basic map generation, this docker will run twice. The first pass generates the map
while the second pass will read through the config for any POIs defined (Players, signs, towns, etc...)

Here is an example of running Overviewer:

```bash
docker run -ti --rm -v /volumes/mc-web-output:/mcmap -v /volumes/minecraft-server-root:/minecraft:ro overviewer
```

It is recommended that you mount your minecraft world as `ro` so that you can ensure overviewer does
not modify any files and this can be done on a running minecraft server.


After the execution is complete, a full map with an index.html file will be generated in the path used
for `/mcmap`.
