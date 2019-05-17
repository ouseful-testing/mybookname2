---
title: 'Home'
prev_page:
  url: 
  title: ''
next_page:
  url: https://github.com/jupyter/jupyter-book
  title: 'GitHub repository'
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---
# Introduction

Proof of concept Jupyter Books site generated (at the moment) from markdown files.

Markdown files created via an XSLT transform of OU-XML.

OU-XML is a structured document format used to represent Open University course materials. OU-XML documents act as the original source document for OU course material published via the OU VLE, as well as print.

OU-XML is also the source format for courses published on OpenLearn.

This site is based on a transformation of the OU-XML source document that underpins the OpenLearn [Learn to Code for Data Analysis](https://www.open.edu/openlearn/ocw/course/view.php?id=4762) course.

The markdown created from the OU-XML transformation can also be parsed by Jupytext to create Jupytrer notebook / `.ipynb` files. Jupyter Book can also create book sites from `.ipynb` so the next step is to convert `.md` to `.ipynb` and then republish the site on that basis.

The next step will then be to add support for Binderhub on the back end so that code / notebooks are in principle executable.

I am so tired. So that'll have to be all for now...