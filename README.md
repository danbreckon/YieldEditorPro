# Yield Editor Pro — Web

A free browser page for cleaning combine yield-monitor data. Drop a file, run Clean this field, check the map, and send the cleaned file. No account. A shapefile, a zip, or a text file stays in the browser. A Precision Planting harvest `.2020` is sent only to the reader on that computer, not to a server.

Dan Breckon and Cory Weber are the authors. Cory Weber wrote the original page. Dan Breckon added the automatic clean and the harvest `.2020` reader.

The current page is `index.html` in this repo. Open that file, or the copy inside YieldEditor-with-2020.zip. The copy at <https://coryweber1988.github.io/YieldEditorPro/> is the original author's hosted page and does not have the automatic pass.

## Open a file

A shapefile, a zip of a shapefile, AgLeader advanced text, a delimited text file, or GeoJSON opens in the page. A John Deere harvest shapefile needs the `.shp`, `.dbf`, and `.shx` together. The `.prj` should come with them. The page will not take the `.shp` alone.

A Precision Planting harvest `.2020` needs the local reader. Extract YieldEditor-with-2020.zip and double-click Open Yield Editor, not the page. The steps are in [Read-me-2020.txt](Read-me-2020.txt). Planting and sprayer `.2020` files are not read yet. A raw John Deere display card is not read yet. The harvest shapefile that display writes is the path that works today.

## Automatic clean

Clean this field is the first action. It estimates the flow delay, then runs the other automatic cuts, and writes the result into the filter boxes. Adjust is there if a box needs to move.

The delay search uses opposing passes. Points within one header of the field edge are left out, and a short fragment is left out. Each direction block is scored on its own. The delay is the point-weighted average of those blocks, to the half second. If the blocks disagree by more than 6 seconds, the delay stays 0. A new file clears the boxes from the last field.

Moisture delay and start and end of pass are not set by this pass. Hillcrest 2025 is a known miss for the delay. On a `.2020`, a delay the monitor already applied is reported, and the search still runs. Overlap stays off when the file has no header width.

## What the page can do

- Import AgLeader advanced text, delimited CSV, TXT, or DAT with a header row, GeoJSON, and shapefiles. Common column names are detected. The mapping can be overridden.
- Dry yield and wet yield are separate columns, so a file with a flow rate instead of a per-area rate can still be mapped.
- Balance by date, by machine, and by moisture, against a base group.
- The USDA Yield Editor filter set: flow delay, start and end of pass, min and max speed, smooth speed, min swath, min and max yield, local standard deviation, a position box, and a drawn exclusion. The fixed order or a dragged order can be used.
- Post-cal scales the cleaned file to a scale ticket, an elevator receipt, or a weigh-wagon total.
- A boundary can clip a GeoTIFF export. The raster is inverse distance or ordinary kriging.
- Export CSV, GeoJSON, a zipped shapefile, or AgLeader text. Full columns, or the cleaned values written back under the original names.
- Save the mapping, filters, balance, and post-cal as a small JSON file and load it on a similar file later.
- A summary can be downloaded as Markdown or HTML.

## Not in yet

- A planting `.2020` and a sprayer `.2020`. When those are added, the default map is one point per second for the whole implement, with a per-row layer behind it. The first sprayer layer is applied rate.
- A raw John Deere display card. The plugin has to be licensed before that drop can work. Until then, use the harvest shapefile.

## Getting started

For a shapefile or a text file, download `index.html` and open it in Chrome, Firefox, Edge, or Safari. Nothing else is installed. The page loads Leaflet, PapaParse, JSZip, and shp.js from cdnjs the first time, so that first open needs a network. The yield file stays in the browser.

For a harvest `.2020`, use the zip and [Read-me-2020.txt](Read-me-2020.txt). The page alone cannot read that format.

## Using it

1. Drop the file.
2. Clean this field. The result line names the delay, the cuts that ran, and how many points remain.
3. Check the map. Adjust is there if a cut needs to move. Show the file before cleaning compares the raw file.
4. Send the shapefile, or export another format from the export tab.

The other tabs are still there: import and column mapping, balance, the individual filters, post-cal, a boundary, and the summary.

## Attribution — USDA Yield Editor

The filter, balance, and calibrate workflow, and the names of the cuts, come from Yield Editor, written by USDA Agricultural Research Service, Cropping Systems and Water Quality Research Unit, Columbia, Missouri. The paper this page follows is Sudduth and Drummond, 2007, Agronomy Journal 99:1471–1482. The delay search follows the later pass-to-pass method. This project is not a USDA product, and it is not endorsed by USDA.

## License

AGPLv3. See [LICENSE](LICENSE). The USDA method named above is separate from that license.

## Acknowledgments

Loaded from [cdnjs](https://cdnjs.com/):

- [Leaflet](https://leafletjs.com/) for the map
- [PapaParse](https://www.papaparse.com/) for delimited text
- [JSZip](https://stuk.github.io/jszip/) for a zipped shapefile
- [shp.js](https://github.com/calvinmetcalf/shapefile-js) for shapefile import

A harvest `.2020` is read by the Precision Planting ADAPT plugin, version 6.2.1, inside the local reader. That plugin is not part of this repo.

## Roadmap

- Planting and sprayer `.2020` files, mapped as above.
- A raw John Deere display card, once the licensed plugin can be used.
- Start and end of pass on the automatic clean, after it has been checked on real fields.
