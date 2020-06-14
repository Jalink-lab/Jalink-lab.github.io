## Single-Molecule Localization Microscopy Tools

Here you find several [Fiji](https://fiji.sc) scripts and plugins to perform automated (batch) processing of Single-Molecule Localization Microscopy (SMLM) datasets, using the ImageJ plugin [ThunderSTORM](https://zitmen.github.io/thunderstorm/).
ThunderSTORM is a very useful tool for analysis and visualization of localization microscopy data. However, it doesn't have much functionality for batch processing, and it misses other necessary processing steps, like temporal background subtraction and chromatic aberration correction for multi-color datasets.
We have developed some tools to automate these processes.

## Download the complete package:
### 1. ImageJ1 macro [SMLM_process_folder.ijm](https://raw.githubusercontent.com/Jalink-lab/SMLM-macro/master/SMLM_process_folder.ijm)
### 2. Plugin [Temporal Median Background Subtraction](https://github.com/Jalink-lab/Temporal-Median-Background-Subtraction/releases/download/v2.2/TemporalMedian-2.2.jar)
### 3. Plugin [Chromatic Aberration Correction](https://github.com/Jalink-lab/Chromatic-Aberration-Correction/releases/download/v1.12/Chromatic-Aberration-Correction-1.12.jar)
### 4. Plugin [ImageJSON](https://github.com/Jalink-lab/ImageJSON/releases/download/v1.0/ImageJSON-1.0.0.jar)

### Installation instructions
Download the plugin .jar files (nr. 2,3 and 4) and place in the Fiji plugins folder. Download the macro (nr. 1), drag into the Fiji window and click Run. Dependencies: [ThunderSTORM](https://zitmen.github.io/thunderstorm/) and [Bio-Formats](https://imagej.net/Bio-Formats).

## Detailed descriptions (links to the repositories)

### [SMLM_process_folder](https://github.com/Jalink-lab/SMLM-macro/)
This macro is essentially a wrapper around the ImageJ plugin [ThunderSTORM](https://zitmen.github.io/thunderstorm/).
It processes all time-lapse images in a folder. Images are opened using Bio-Formats. In case the chosen file format is `.lif` (Leica Image Format) multiple series within a file are processed.
The most important settings of ThunderSTORM can be set using script parameters. For clarity we have chosen to not include all parameters. Other parameters are either set to reasonable default values, and/or are taken over from the current ThunderSTORM settings. Some can be changed in the top of the macro code.

![Parameters dialog](/images/SR_postprocess_dialog_screenshot_small.png)

We have added a few useful features, described below.

Disclaimer: The macro was initially designed for analyzing data from a Leica SR-GSD microscope. It certainly works for separate `.tif` files, and most probably other Bio-Formats compatible file formats as well. Currently chromatic aberration can only be automatically applied with the macro if the (excitation) wavelengths are set to 488 nm, 532 nm, or 642 nm, where the first two are mapped to the latter. These wavelengths should either be in the metadata (for `.lif` files), or the filename (excluding extension) should end with `488`, `532` or `642`. If you use different wavelengths, a workaround is to rename your files accordingly, and thus trick the macro into _thinking_ that you are using those wavelengths. We are working on a more general solution.


### [Temporal Median Background subtraction](https://github.com/Jalink-lab/Temporal-Median-Background-Subtraction)
In SMLM, the localization precision critically depends on the (Gaussian) fit of the underlying pixel data of single emitting fluorohore. SMLM datasets sometimes contain a significant structured background, usually originating from out-of-focus, continuously emitting fluorophores attached to cellular structures or cellular auto-fluorescence. Such background is often present in PALM, and in dSTORM imaging with non-perfect blinking dyes (too short dark state).
Due to bleaching and other effects the background changes over time. Since this happens on a much slower time scale then the blinking of fluorophores, and fluorophores are only 'on' for a relatively short time, the background can be estimated with a temporal median filter (see [Hoogendoorn et al.](https://www.nature.com/articles/srep03854)).

We have written a fast implementation that calculates for every pixel a sliding median over time, and subtracts the result from the original. Performing Temporal Median Background Subtraction can yield a dramatically improved superresolved image.

There is a [Imglib2 version](https://github.com/Jalink-lab/Temporal-Median-Background-Subtraction/releases/tag/v3.2) as well that uses less memory, but it is ~2.5 times slower than the [ImageJ1 version](https://github.com/Jalink-lab/Temporal-Median-Background-Subtraction/releases/tag/v2.2).

### [Chromatic Aberration Correction](https://github.com/Jalink-lab/Chromatic-Aberration-Correction/)
Because of the high localization precision in SMLM, chromatic aberrations are inevitable when imaging multiple colors.
We provide tools to transform the `x` and `y` localization coordinates from different wavelengths using affine transformations. The required transformation matrices to map one color onto another can be generated with localization data from multicolor beads. See the [repository](https://github.com/Jalink-lab/Chromatic-Aberration-Correction/) for more information.


### [ImageJSON plugin](https://github.com/Jalink-lab/ImageJSON)
This plugin is used to save all the settings (both SMLM_process_folder-specific and ThunderSTORM-specific) for every processed file in JSON format for easy indexing by other software.

Copyright (c) 2017-2020. All code was developed by Rolf Harkes and Bram van den Broek, with testing by Leila Nahidiazar, in the [Kees Jalink lab](https://jalinklab.nl), at the [The Netherlands Cancer Institute](https://nki.nl)

