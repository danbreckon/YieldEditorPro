# Contributing to Yield Editor Pro — Web

Thanks for your interest in improving this tool. It's a young, single-maintainer project, so please keep pull requests focused and reasonably small — easier to review, easier to merge.

## Reporting bugs

Open an [issue](../../issues) and include, where possible:

- What you were trying to do, and what happened instead.
- The yield monitor / file format involved (e.g. "AgLeader Advanced Text export from an XXXX monitor"), if relevant.
- Browser and OS.
- A sample file that reproduces the problem, if you're able to share one — **please scrub or use non-sensitive test data**, since issues are public. A few rows is usually enough.
- Any error shown in the browser console (F12 → Console tab).

## Suggesting features

Open an issue describing the use case — what you're trying to accomplish, and why the current tool doesn't cover it. Screenshots of the relevant tab, or an example of the file structure you need to support, help a lot.

## Submitting changes

1. Fork the repo and create a branch off `main`.
2. The page is a single `index.html` file, so open it in a browser to test. The harvest `.2020` reader is a separate local program and is not in this repo. A change to the page can be tested with a shapefile. A change to the reader needs the zip.
3. Before opening a pull request:
   - Check the browser console for errors on a real (or realistic sample) dataset, covering the Import → Balance → Filters → Post-Cal → Boundary → Export flow if your change touches the pipeline.
   - If you changed the filter set, balancing, calibration, or export logic, please test with a small file that has GPS/timestamp/yield columns representative of a real yield monitor.
   - Keep the file dependency-free beyond what's already loaded from cdnjs.cloudflare.com (Leaflet, PapaParse, JSZip, shp.js) unless there's a strong reason to add something new — the point of this tool is that it's one file anyone can open with no install.
4. Describe what changed and why in the pull request description. For anything that changes the pipeline's numeric output (filters, balancing, calibration, interpolation), a brief before/after on a test file is very helpful.

## Scope

This project follows the general filter/balance/calibrate workflow of the original USDA-ARS Yield Editor (see the README's Attribution section) — if you're proposing a new filter or calibration step, a link to the agronomic or statistical reasoning behind it is helpful context for review.

## Licensing of contributions

This project is licensed under AGPLv3 (see [LICENSE](LICENSE)). By submitting a pull request, you agree to the terms of the [Contributor License Agreement](CLA.md) (or, if contributing on behalf of a company, the [Entity CLA](CLA-ENTITY.md)) — you keep your copyright, but grant the Project Owner a broad license to use, distribute, and relicense your contribution, including under different license terms in the future if the Project's license ever changes. A CLA Assistant bot checks this automatically: on your first pull request it will ask you to reply with *"I have read the CLA Document and I hereby sign the CLA"* — your signature is then recorded and you won't be asked again.

## Questions

Open an issue on this repo. The authors are Dan Breckon and Cory Weber. Cory Weber, coryweber1988@gmail.com, wrote the original page. Dan Breckon wrote the PCDI flow-delay search in this project.
