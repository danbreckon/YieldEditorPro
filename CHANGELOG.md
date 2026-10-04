# Changelog

All notable changes to this project are documented here. Dates are in `YYYY-MM-DD`.

## [2026-10-04]

### Changed
- The public page no longer offers the Precision Planting reader. A `.2020` needs a reader licensed on that computer. The plugin is not in this repo, and it is not part of the gift.
- Copyright notices name Cory Weber and Dan Breckon. Each keeps the copyright in the part he wrote. The contributor grant still names Cory Weber as Project Owner until both authors sign a change.
- The USDA note no longer calls the original Yield Editor public domain. USDA's own download terms apply to USDA's software.
- The ignore file is `.gitignore`. A plugin zip, an executable, and farm data are ignored.

## [2026-10-03]

### Added
- Clean this field. One action runs the automatic pass: flow delay, then the other automatic cuts. The result is written into the filter boxes. Adjust is there if a box needs to move.
- Flow-delay estimate, written by Dan Breckon. This is his PCDI implementation for this project, after Lee, Sudduth, Drummond, and Chung, 2012. Passes are grouped by direction. Points within one header of the field edge are left out, and a short fragment is left out. Each block is scored on its own. The delay is the point-weighted average of the blocks, to the half second. If the blocks disagree by more than 6 seconds, the delay stays 0.
- A new file clears the filter boxes from the last field.
- A harvest `.2020` can be sent to a reader that is already licensed on that computer. The page itself cannot read that format, and this repo does not ship the reader. See Read-me-2020.txt.

### Changed
- The read progress sits in the middle of the map, with the percent and the time left. It closes when the field is drawn. Clicking it also closes it.
- The docs now match the page: Clean this field is the first action, a `.2020` is harvest only, and a raw John Deere card is not read.

### Known
- Hillcrest 2025 is a miss for the delay estimate. Moisture delay is not set by the automatic pass.
- A `.2020` read is harvest only. Planting and sprayer files are not read yet. A raw John Deere display card is not read. Overlap stays off when the file has no header width.

## [2026-10-02]

### Changed
- Fixed polygon select tool.  System was drawing polygon but not actually being used to delete features.

## [2026-09-16]

### Added
- Open-source release: README, AGPLv3 license, contributing guide, and this changelog.
- Drag-to-reorder filter list, with a checkbox to switch between the traditional fixed USDA filter order and a user-defined order.
- Streamlined export column-set option — export just the cleaned wet/dry/moisture values under their *original* column names, alongside the existing "Full" (original + cleaned columns) export.
- Ordinary Kriging as an alternative to IDW for GeoTIFF raster interpolation, with an optional manual variogram range.
- Esri Aerial Imagery Hybrid basemap (imagery + labels overlay), plus OpenTopoMap and Humanitarian OSM basemap options.
- In-app Help tab sections: tool overview, USDA Yield Editor attribution, and developer/contact info.

### Changed
- Removed CARTO basemap options (they require an API key, which doesn't fit a single keyless HTML file).
- Moved the map zoom (+/−) control from the top-left to the bottom-left, so it no longer overlaps the "Colour map by" panel.

### Earlier
- Separate, independently-optional Dry/Processed Yield and Wet/Unprocessed Yield column mapping, with a user-chosen primary yield column driving filters and pass-outlier detection.
- Core pipeline: Import (AgLeader Text / CSV / GeoJSON / Shapefile), column-mapping auto-detection, date/machine/moisture Balance, the full USDA Yield Editor Filter set, Post-Cal scale-total calibration, boundary import, and CSV/GeoJSON/Shapefile/AgLeader Text/GeoTIFF export.
- Session save/load, and a downloadable Markdown/HTML summary report.
