# Yield Editor Pro — Web

A free, browser-based tool for cleaning combine yield-monitor data — importing raw yield files, correcting machine/date/moisture calibration drift, filtering out bad points, truing the result up to a known scale-ticket total, and exporting cleaned data or an interpolated yield map. It's a single self-contained HTML file: no install, no account, no server, and no data ever leaves your browser.

**[Launch the tool »] https://coryweber1988.github.io/YieldEditorPro/



---


## Automatic clean

Clean this field runs the automatic pass and writes the result into the filter boxes. The flow delay is estimated from opposing passes, with the field edge and short fragments left out. If the direction blocks disagree by more than 6 seconds, the delay stays 0. Moisture delay and start/end pass delay are not set by this pass.

A shapefile, a zip, or a text file opens in the page. A Precision Planting .2020 file needs the local reader. Extract YieldEditor-with-2020.zip and double-click Open Yield Editor, not the page. The steps are in [Read-me-2020.txt](Read-me-2020.txt).

## Features

- **Import** — AgLeader Advanced Text, delimited CSV/TXT/DAT with a header row, GeoJSON, and Shapefiles (zipped or loose `.shp`/`.dbf`/`.shx`/`.prj`). Auto-detects common column names, with manual override.
- **Column mapping** — separate, independently-optional Dry/Processed Yield and Wet/Unprocessed Yield columns, so monitors that log a raw flow-rate signal alongside (or instead of) a per-area rate are both supported.
- **Balance** — date balancing and machine balancing (mean-ratio scaling against a base group), plus moisture-ratio-based balancing for a machine whose moisture sensor is out of calibration.
- **Filters** — the standard USDA Yield Editor filter set (grain-flow delay, start/end pass delay, min/max velocity, smooth velocity, min swath, min/max yield, std. deviation of yield, position box, manual polygon exclusion), each independently toggleable. Filters can run in the traditional fixed order, or you can drag them into a custom order and apply them that way instead.
- **Post-Cal** — a final single-factor scale-up against a real-world total (scale ticket, elevator receipt, weigh-wagon reading).
- **Boundary & GeoTIFF export** — import a field boundary to clip a GeoTIFF raster export, interpolated with either Inverse Distance Weighting (IDW) or Ordinary Kriging.
- **Export** — CSV, GeoJSON, Shapefile (zipped), and AgLeader Text, with a choice between a **Full** column set (original + cleaned columns) or a **Streamlined** column set (just the cleaned wet/dry/moisture values, written back under the original column names, so the output's structure closely matches the source file's).
- **Session save/load** — save your column mapping, filter, balance, and Post-Cal settings as a small JSON file to reuse on a similar dataset later.
- **Summary report** — a downloadable Markdown or HTML record of the source file, mapping, every pipeline stage's record count, balancing/calibration factors, and any GeoTIFF exports made.

## Getting started

There's nothing to install. Either:

- **Use the hosted version** at the link above, or
- **Run it locally** — download `index.html` from this repo and open it in any modern browser (Chrome, Firefox, Edge, Safari).

The app itself runs entirely client-side — your data is processed in your browser and is never uploaded anywhere. It does load a few JavaScript libraries (Leaflet for mapping, PapaParse for CSV parsing, JSZip for zipped Shapefile export, shp.js for reading Shapefiles) from a public CDN (cdnjs.cloudflare.com), so an internet connection is needed the first time the page loads in a session, even though your yield data itself stays local.

## Hosting on GitHub Pages

This repo is set up to be served directly by GitHub Pages, no build step required:

1. Push this repo to GitHub (see below if you haven't already).
2. In the repo, go to **Settings → Pages**.
3. Under **Build and deployment → Source**, choose **Deploy from a branch**.
4. Set **Branch** to `main` (or whichever branch you push to) and folder to **/ (root)**, then **Save**.
5. GitHub will publish the site at `https://YOUR-GITHUB-USERNAME.github.io/YOUR-REPO-NAME/` within a minute or two — because the tool is `index.html` at the repo root, that URL loads it directly.
6. Come back and update the link at the top of this README once it's live.

If you'd rather push from the command line:

```bash
git init
git add .
git commit -m "Initial commit — Yield Editor Pro Web"
git branch -M main
git remote add origin https://github.com/CoryWeber1988/YieldEditorPro/.git
git push -u origin main
```

Then enable Pages as described above.

## Usage guide

The tabs run roughly in the order you'd use them:

1. **Import** your data and map its columns (Longitude/Latitude are required; Timestamp and Machine ID unlock most of the rest of the tool).
2. **Balance** out machine/date/moisture calibration differences, if needed.
3. **Filters** — enable and configure the filters you want, then **Apply All Filters**.
4. **Post-Cal** — optionally true the result up to a known scale total.
5. **Boundary** — optionally import a field boundary.
6. **Export** — download cleaned data (CSV / GeoJSON / Shapefile / AgLeader Text) and/or a GeoTIFF raster.
7. **Summary** — review and download a record of everything the pipeline did.

Re-running any tab's Apply button recomputes the whole pipeline in order — you don't need to reapply earlier tabs after changing a later one. The in-app **Help** tab has a full walkthrough of every option.

## Attribution — USDA Yield Editor

The filter/balance/calibrate workflow and terminology this tool follows — Start/End Pass Delay, Grain Flow Delay, Smooth Velocity, Std. Deviation of Yield, and the rest of the filter set — come from the original **Yield Editor** desktop software developed by USDA's Agricultural Research Service (ARS), Cropping Systems and Water Quality Research Unit, Columbia, Missouri, as part of its precision-agriculture research program.

This project is a separate, independent web reimplementation built to work from a browser with no install. **It is not official USDA software and is not endorsed by or affiliated with USDA/ARS.**

Official USDA Yield Editor download and documentation: [ars.usda.gov — Yield Editor](https://www.ars.usda.gov/research/software/download/?softwareid=370&modecode=50-70-10-00). As software produced by the U.S. federal government, the original Yield Editor is generally in the public domain within the United States; see the disclaimer bundled with that official download for its exact terms, and please credit "USDA-ARS Yield Editor" when referencing the underlying methodology.

## Developer & contact

Built by **Cory Weber** ([Cory Weber Ag Tech](https://github.com/CoryWeber1988), developed with the assistance of Claude (Anthropic). For questions, bug reports, or feature requests, contact **coryweber1988@gmail.com**, or open an [issue](../../issues) on this repo.

## Contributing

Contributions, bug reports, and feature suggestions are welcome — see [CONTRIBUTING.md](CONTRIBUTING.md).

## License

This project is licensed under the [GNU Affero General Public License v3.0 (AGPLv3)](LICENSE). In short: anyone can use, modify, and redistribute it — including commercially — but any distributed modified version, **and any modified version made available to users over a network** (e.g. a hosted/SaaS fork), must also make its complete source code available under AGPLv3. This is meant to close off the "quietly turn it into a closed, hosted product" path while still allowing commercial use. See the [Attribution](#attribution--usda-yield-editor) section above regarding the underlying USDA methodology this tool implements, which is separate from this project's own AGPLv3 license.

## Acknowledgments

Built with these open-source libraries, loaded from [cdnjs](https://cdnjs.com/):

- [Leaflet](https://leafletjs.com/) — interactive map
- [PapaParse](https://www.papaparse.com/) — CSV parsing
- [JSZip](https://stuk.github.io/jszip/) — zipped Shapefile export
- [shp.js](https://github.com/calvinmetcalf/shapefile-js) — Shapefile import

## Roadmap of Features

Planned feature enhancements and additions for the tool are:

- potential use of ADAPT framework at https://github.com/AgGateway-ADAPT to output files supported by online grower facing platforms.  Not all platforms will accept shapefile or CSV which may limit growers who would like this data back within their regular tools
