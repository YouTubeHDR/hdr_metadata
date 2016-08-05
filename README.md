# Matroska Colour Metadata Ingestion Utility

The utilities provided in this repository can be used to ingest colour metadata into matroska containers. This tool is derived from on the open source project [MKVToolNix](https://github.com/mbunkus/mkvtoolnix). 
For more details about thecolour metadata in Matroska or WebM containers, 
see [here](http://www.webmproject.org/docs/container/#location-of-the-colour-element-in-an-mkv-file)
and [here](http://www.webmproject.org/docs/container/#colour).

Two utilities are provided
* mkvmerge is used to ingest colour metadata into matroska containers.
* mkvinfo can be used to review the metadata of a matroska file and to confirm the metadata is correctly ingested.

Binaries of the two utilities are provided for Windows and MacOS.
* On Windows
  * Use the 32bits executables from [/windows/32bits](/windows/32bits) for running on i686 CPUs
  * Use the 64bits executables from [/windows/32bits](/windows/64bits) for running on x86 CPUs.
* On MacOS
  * Use the mkvmerge.app and mkvinfo.app from [/macos](/macos) 

# Ingest metadata with `mkvmerge` 
* On Windows
  * run mkvmerge.exe from command line console
* On MacOS
  * run mkvmerge in the mkvmerge.app folder from terminal as
  ```
  ./mkvmerge.app/Contents/MacOS/mkvmerge ...
  ```
The complete manual about the command line can be found [here](https://mkvtoolnix.download/doc/mkvmerge.html).
You may also get the list of all flags by runing `mkvmerge -help`. 
For example, to ingest color metadata into a video named input.mov, you may use the following command.
```shell
 ./src/mkvmerge \
      -o output.mkv\
      --colour-matrix 0:9 \
      --colour-range 0:1 \
      --colour-transfer-characteristics 0:16 \
      --colour-primaries 0:9 \
      --max-content-light 0:1000 \
      --max-frame-light 0:300 \
      --max-luminance 0:1000 \
      --min-luminance 0:0.01 \
      --chromaticity-coordinates 0:0.68,0.32,0.265,0.690,0.15,0.06 \
      --white-colour-coordinates 0:0.3127,0.3290 \
      input.mov 
```
Then the metadata will be written to output.mkv file. 


# (Optional) Review ingested with `mkvinfo` 
* On Windows
  * run mkvinfo.exe from command line console
* On MacOS
  * run mkvinfo in the mkvmerge.app folder from terminal as
  ```
  ./mkvinfo.app/Contents/MacOS/mkvmerge ...
  ```
To check the metadata of output file, you may run ./mkvinfo out.mkv to get the following results (colour metadata is shown in blue colour):
```
...
|  + Video track
|   + Pixel width: 1920
|   + Pixel height: 1080
|   + Display width: 1920
|   + Display height: 1080
|   + Video colour
|    + Colour matrix: 1
|    + Bits per channel: 12
|    + Horizontal chroma subsample: 1
|    + Vertical chroma subsample: 1
|    + Horizontal Cb subsample: 1
|    + Vertical Cb subsample: 1
|    + Colour range: 3
|    + Colour transfer: 13
|    + Colour primaries: 22
|    + Max content light: 1000
|    + Max frame light: 1200
|    + Video colour mastering metadata
|     + Red colour coordinate x: 0.01
|     + Red colour coordinate y: 0.01
|     + Green colour coordinate x: 0.02
|     + Green colour coordinate y: 0.02
|     + Blue colour coordinate x: 0.03
|     + Blue colour coordinate y: 0.03
|     + Max luminance: 999.99
|     + Min luminance: 0.01
...
```
# Supported input format for HDR videos
For HDR videos, the only input format we supported is quicktime (`.mov` files) with 
Apple Prores video stream and AAC audio stream.
