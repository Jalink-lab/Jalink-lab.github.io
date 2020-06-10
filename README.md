## Welcome to Jalink Lab.

Here you can find several [Fiji](https://fiji.sc) scripts for automated reconstruction of Single-Molecule Localization Microscopy (SMLM) images.

# SR_postProcess.ijm
This macro is basically a wrapper around the ImageJ plugin [ThunderSTRORM](https://zitmen.github.io/thunderstorm/).
It allows processing multiple blinking movies in a folder. In the dialog the most important settings of ThunderSTORM can be set. (Other parameters are set to default, and/or can be changed in the macro code before running. _(@rharkes nog even checken of dit waar is?)_

We have included a few convenient extras, such as [Temporal Median Background subtraction](https://www.nature.com/articles/srep03854) and Chromatic Aberration Correction sing affine transformations.

All settings (both from this macro and ThunderSTORM-specific settings) are saved in JSON files.



Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/Jalink-lab/Jalink-lab.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
