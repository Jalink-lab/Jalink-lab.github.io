## Single-Molecule Localization Microscopy Tools

We have created [Fiji](https://fiji.sc) scripts and plugins for automated (batch) processing of Single-Molecule Localization Microscopy (SMLM) datasets, using [ThunderSTORM](https://zitmen.github.io/thunderstorm/).

## Download the complete package:
### 1. ImageJ1 macro [SMLM_process_folder.ijm](https://raw.githubusercontent.com/Jalink-lab/SMLM-macro/master/SMLM_process_folder.ijm)
### 2. Plugin [Temporal Median Background Subtraction](https://github.com/Jalink-lab/SMLM-macro/blob/master/SMLM_process_folder.ijm)
### 3. Plugin [Chromatic Aberration Correction](https://github.com/Jalink-lab/Chromatic-Aberration-Correction/releases/download/v1.12/Chromatic-Aberration-Correction-1.12.jar)
### 4. Plugin [ImageJSON](https://github.com/Jalink-lab/ImageJSON/releases/download/v1.0/ImageJSON-1.0.0.jar)

### Installation instructions
Download the plugins .jar files (nr. 2,3 and 4) and place in the Fiji plugins folder. Download the macro, drag into the Fiji window and click Run. [ThunderSTORM](https://zitmen.github.io/thunderstorm/) is a prerequisite.

## Detailed descriptions (links to the repositories)

### [SMLM_process_folder](https://github.com/Jalink-lab/SMLM-macro/)
This macro is basically a wrapper around the ImageJ plugin [ThunderSTORM](https://zitmen.github.io/thunderstorm/), still a very useful tool for SMLM analysis. However, ThunderSTORM doesn't have much functionality for batch processing.
This macro processes all blinking time-lapse images in a folder. If the file format is Leica's .lif, multiple series in one file are processed.
In the dialog the most important settings of ThunderSTORM can be set. (Other parameters are taken from ThunderSTORM, and/or can be changed in the macro code before running.

We have included a few convenient extras, such as:

### [Temporal Median Background subtraction](https://github.com/Jalink-lab/Temporal-Median-Background-Subtraction/releases/download/v2.2/TemporalMedian-2.2.jar)
In SMLM, the localization precision critically depends on the (typically) Gaussian fit. However, super-resolution datasets sometimes contain significant non-sparse, structured background components. Such background usually originates from out-of-focus, continuously emitting fluorescent molecules attached to cellular structures or cellular auto-fluorescence, and is often present with dSTORM imaging of dyes with non-perfect blinking properties, and PALM.
Due to bleaching and other effects the structured background changes slowly over time, much slower than the blinking fluorophores. It can be estimated with a temporal median filter (see [Hoogendoorn et al.]https://www.nature.com/articles/srep03854). We have written a fast implementation that calculates a sliding median for every pixel over time with a large time window, and subtracts it from the original. Performing Temporal Median Background Subtraction can yield a dramaticcally better superresolved image.

There is a [Imglib2 version](https://github.com/Jalink-lab/Temporal-Median-Background-Subtraction/releases/tag/v3.2) as well, but it is slower than the [ImageJ1 version](https://github.com/Jalink-lab/Temporal-Median-Background-Subtraction/releases/tag/v2.2). We recommend to use the latter.

### [Chromatic Aberration Correction](https://github.com/Jalink-lab/Chromatic-Aberration-Correction/releases)
Because of the high localization precision in SMLM, chromatic aberrations are inevitable when imaging multiple colors.
We provide tools to transform the x,y localizations from different wavelengths using affine transformations. The required transformation matrices to map one color onto another can be generated with localization data from multicolor beads.
N.B. We designed this plugin for the Leica SR-GSD microscope. Currently chromatic aberration can only be applied if the (excitation) wavelengths are set to 488 nm, 532 nm, or 642 nm, where the first two are mapped to the latter. (If you have another system you can still trick the system, so you don't actually have to use these wavelength.)

### [ImageJSON plugin](https://github.com/Jalink-lab/ImageJSON)
This plugin is used to save all the settings (both SMLM_process_folder-specific and ThunderSTORM-specific) for every prcessed file in JSON format for easy indexing by other software.

(c) 2020. All code was developed by Rolf Harkes and Bram van den Broek, in the [Kees Jalink lab](https://jalinklab.nl), at the [The Netherlands Cancer Institute](https://nki.nl)

