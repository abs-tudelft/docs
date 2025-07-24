# ABS Group Project Documentation

This repository contains an MkDocs book with documentation for various projects by ABS students and researchers in a more centralized way then semi-interlinked readmes.

Right now it contains documentation of:
- [Tydi-spec](https://github.com/abs-tudelft/tydi)
- [Tydi-Chisel](https://github.com/abs-tudelft/Tydi-Chisel)
- [Tydi-Clash](https://github.com/The-Redstar/tydi-clash)
- [Tywaves](https://github.com/rameloni/tywaves-chisel)
- ChiselSlicer (has no public repo yet)

## Building the book

Install [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) and [Mkidocs-Macros](https://mkdocs-macros-plugin.readthedocs.io/) using pip (possibly in a virtual environment for your convenience).

```shell
pip install mkdocs-material mkdocs-macros-plugin
```

Make sure the install location is in your path, then run

```shell
mkdocs serve
```

and access the book at http://127.0.0.1:8000/.
