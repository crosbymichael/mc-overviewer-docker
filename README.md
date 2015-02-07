# Minecraft Overviewer

Generate a Google Maps like map of your minecraft world.  Documentation for overview can be
found [here](http://overviewer.org/).


## Usage

This Dockerfile requires two volumes owned by UID:GID 1 ( default ).  One volume must be mounted 
undert `/minecraft` which contains a world directory for the world that you wish to create a
map of.  The other is the output directory that will contain the generated map mounted under
`/mcmap`.

Here is an example:

```bash
docker run -ti --rm -v /volumes/mcworld:/mcmap -v /volumes/minecraft-family:/minecraft:ro overviewer
```

It is recommended that you mount your minecraft world as `ro` so that you can ensure overviewer does
not modify any files and this can be done on a running minecraft server.


After the execution is complete, a full map with an index.html file will be generated in the path used
for `/mcmap`.
