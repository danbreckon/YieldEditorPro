# Yield Editor Pro — Web

A free browser page for cleaning combine yield-monitor data. Drop a file, run Clean this field, check the map, and send the cleaned file. No account. A shapefile, a zip of a shapefile, or a text file stays in the browser. A Precision Planting harvest `.2020` is not read by this page. If a reader licensed from Precision Planting is already on that computer, the page can send the file to that reader. It does not send the file to a server.

Dan Breckon and Cory Weber are the authors. Cory Weber wrote the original page. Dan Breckon wrote the automatic clean, the PCDI flow-delay search in this project, and the harvest `.2020` reader call. Each keeps the copyright in the part he wrote.

The current page is `index.html` in this repo. Open that file. The copy at <https://coryweber1988.github.io/YieldEditorPro/> is the original author's hosted page and does not have the automatic pass.

## Give it away

This page is free. Copy it, send it, and put it on a stick. No account, no fee, no limit on fields. A consultant can hand the file to a grower. The license is AGPLv3, so a copy that is changed and offered to others has to stay free too. A hosted copy of a changed page has to offer that same source.

The Precision Planting 20|20 ADAPT plugin is not part of this gift. It is not in this repo, and this repo does not offer a zip that contains it. That plugin is theirs. Do not attach it to a release or hand it on with the page. A wider distribution needs written leave from Precision Planting. The page in this repo is the part anyone can take.

The page does not ask for money. If the work saved you a night and you want to pay Dan Breckon for it, open an issue on this repo and say so. He will send the way to pay. Paying does not unlock a feature, and it does not include the plugin.

## Open a file

A shapefile, a zip of a shapefile, AgLeader advanced text, a delimited text file, or GeoJSON opens in the page. A John Deere harvest shapefile needs the `.shp`, `.dbf`, and `.shx` together. The `.prj` should come with them. The page will not take the `.shp` alone.

A Precision Planting harvest `.2020` needs a reader licensed on that computer. This page cannot install it, and this repo does not ship it. See [Read-me-2020.txt](Read-me-2020.txt). Planting and sprayer `.2020` files are not read yet. A raw John Deere display card is not read yet. The plugin has to be licensed before that drop can work. Until then, use the harvest shapefile that display writes.

## Automatic clean

Clean this field is the first action. It estimates the flow delay, then runs the other automatic cuts, and writes the result into the filter boxes. Adjust is there if a box needs to move.

The delay search uses opposing passes. Points within one header of the field edge are left out, and a short fragment is left out. Each direction block is scored on its own. The delay is the point-weighted average of those blocks, to the half second. If the blocks disagree by more than 6 seconds, the delay stays 0. A new file clears the boxes from the last field.

Start and end of pass are set from the seconds each pass takes to reach steady yield and speed, and to leave it. A side the passes disagree on by more than 6 seconds stays at 0. Moisture delay is not set. Hillcrest 2025 is a known miss for the delay. On a `.2020`, a delay the monitor already applied is reported, and the search still runs. Overlap stays off when the file has no header width.

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

A local call for other programs is in [API.md](API.md). It runs the same clean. It does not send the file anywhere.

## Not in yet

- A planting `.2020` and a sprayer `.2020`. When those are added, the default map is one point per second for the whole implement, with a per-row layer behind it. The first sprayer layer is applied rate.
- A raw John Deere display card. The plugin has to be licensed before that drop can work. Until then, use the harvest shapefile.

## Getting started

Download `index.html` and open it in Chrome, Firefox, Edge, or Safari. Nothing else is installed. The page loads Leaflet, PapaParse, JSZip, and shp.js from cdnjs the first time, so that first open needs a network. The yield file stays in the browser.

A harvest `.2020` is not opened by that download. The reader is separate, and it is not offered here.

## Using it

1. Drop the file.
2. Clean this field. The result line names the delay, the cuts that ran, and how many points remain.
3. Check the map. Adjust is there if a cut needs to move. Show the file before cleaning compares the raw file.
4. Send the shapefile, or export another format from the export tab.

The other tabs are still there: import and column mapping, balance, the individual filters, post-cal, a boundary, and the summary.

## Attribution — USDA Yield Editor

The filter, balance, and calibrate workflow follows Yield Editor, from USDA-ARS in Columbia, Missouri, and the method in Sudduth and Drummond, 2007. The flow-delay search in this project is Dan Breckon's implementation of PCDI, from Lee, Sudduth, Drummond, and Chung, 2012. The method is theirs. The code here is ours. This project is not a USDA product and is not endorsed by USDA. USDA's own download terms apply to USDA's software, not to this page.

Yield Editor is a name used by USDA-ARS. AgLeader, John Deere, FieldView, Precision Planting, and 20|20 are names of their owners. This project is not affiliated with them.

## License

AGPLv3. Copyright (C) 2026 Cory Weber and Dan Breckon. See [LICENSE](LICENSE). The USDA method named above is separate from that license.

## Acknowledgments

Loaded from [cdnjs](https://cdnjs.com/):

- [Leaflet](https://leafletjs.com/) for the map
- [PapaParse](https://www.papaparse.com/) for delimited text
- [JSZip](https://stuk.github.io/jszip/) for a zipped shapefile
- [shp.js](https://github.com/calvinmetcalf/shapefile-js) for shapefile import

A harvest `.2020` can be read only by a Precision Planting ADAPT plugin the user has licensed. That plugin is not part of this repo, and it is not offered for download here.

## Roadmap

- Planting and sprayer `.2020` files, mapped as above, once a licensed reader can supply them.
- A raw John Deere display card, once the licensed plugin can be used.
