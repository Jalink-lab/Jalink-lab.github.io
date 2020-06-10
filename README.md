## Welcome to Jalink Lab.

Here you can find several [Fiji](https://fiji.sc) scripts for automated reconstruction of Single-Molecule Localization Microscopy (SMLM) images.

### [SR_postProcess.ijm](https://test.nl)
This macro is basically a wrapper around the ImageJ plugin [ThunderSTRORM](https://zitmen.github.io/thunderstorm/).
It allows processing multiple blinking movies in a folder. In the dialog the most important settings of ThunderSTORM can be set. (Other parameters are set to default, and/or can be changed in the macro code before running. _(@rharkes nog even checken of dit waar is?)_

We have included a few convenient extras, such as [Temporal Median Background subtraction](https://www.nature.com/articles/srep03854) and Chromatic Aberration Correction sing affine transformations.

All settings (both from this macro and ThunderSTORM-specific settings) are saved in JSON files.
![Macro dialog](images/SR_postprocess_dialog_screenshot.png)
Format: ![Alt Text](url)
