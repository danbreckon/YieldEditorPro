# Contributing to Yield Editor Pro — Web

Thanks for your interest in improving this tool. It's a young project, so please keep pull requests focused and reasonably small — easier to review, easier to merge.

## Reporting bugs

Open an [issue](../../issues) and include, where possible:

- What you were trying to do, and what happened instead.
- The yield monitor / file format involved (e.g. "AgLeader Advanced Text export from an XXXX monitor"), if relevant.
- Browser and OS.
- A sample file that reproduces the problem, if you're able to share one — **please scrub or use non-sensitive test data**, since issues are public. A few rows is usually enough.
- Any error shown in the browser console (F12 → Console tab).

Do not attach a grower's yield file, a Precision Planting plugin, a John Deere plugin, or USDA Yield Editor source.

## Suggesting features

Open an issue describing the use case — what you're trying to accomplish, and why the current tool doesn't cover it. Screenshots of the relevant tab, or an example of the file structure you need to support, help a lot.

## Submitting changes

1. Fork the repo and create a branch off `main`.
2. The page is a single `index.html` file, so open it in a browser to test. The harvest `.2020` reader is not in this repo. A change to the page can be tested with a shapefile.
3. Before opening a pull request:
   - Check the browser console for errors on a real (or realistic sample) dataset, covering the Import → Balance → Filters → Post-Cal → Boundary → Export flow if your change touches the pipeline.
   - If you changed the filter set, balancing, calibration, or export logic, please test with a small file that has GPS/timestamp/yield columns representative of a real yield monitor.
   - Keep the file dependency-free beyond what's already loaded from cdnjs.cloudflare.com (Leaflet, PapaParse, JSZip, shp.js) unless there's a strong reason to add something new — the point of this tool is that it's one file anyone can open with no install.
4. Describe what changed and why in the pull request description. For anything that changes the pipeline's numeric output (filters, balancing, calibration, interpolation), a brief before/after on a test file is very helpful.

## Scope

This project follows the general filter/balance/calibrate workflow of the original USDA-ARS Yield Editor (see the README's Attribution section) — if you're proposing a new filter or calibration step, a link to the agronomic or statistical reasoning behind it is helpful context for review. Do not copy USDA source into the pull request.

## Licensing of contributions

This project is licensed under AGPLv3 (see [LICENSE](LICENSE)). Copyright in the page is held by Cory Weber and Dan Breckon, each in the part he wrote. By submitting a pull request, you agree to the terms of the [Contributor License Agreement](CLA.md) (or, if contributing on behalf of a company, the [Entity CLA](CLA-ENTITY.md)). You keep your copyright. The CLA grants Cory Weber, as Project Owner, a license to use, distribute, and relicense the contribution. That grant does not move the existing copyright, and it does not by itself let either author relicense the other's part. A later change of Project Owner needs a writing signed by both authors.

The CLA check is not running. `cla.yml` is not in `.github/workflows` because the action it names is archived. Until it is enabled, add this comment yourself on your first pull request: *"I have read the CLA Document and I hereby sign the CLA"*.

## Questions

Open an issue on this repo. The authors are Dan Breckon and Cory Weber. Cory Weber, coryweber1988@gmail.com, wrote the original page. Dan Breckon wrote the PCDI flow-delay search in this project.
