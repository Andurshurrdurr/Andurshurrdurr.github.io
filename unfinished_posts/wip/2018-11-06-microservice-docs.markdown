---
layout: post
title: "Scalable Microservice Documentation"
date: 2018-11-06
author: Anders
category: Docs
tags: Sphinx Python Documentation
finished: false
img: covers/
---

# Documentation

Documentation is one of those funny things for developer or engineers. It is
one of the most social things that these creatures do 

## Challanges with documentation

- It is time consuming
- It can be(come) misleading
- It can become unsynced with the source (if you change the code it documents,
  but not the documentation)
- It becomes an ad-hoc operation

## Why document

So with all these challenges, why bother spending time and resources to write
good documentation? Why even write documentation? Plenty of people go through
life without writing good documenation, and plenty of technology just lies in

## Introduction to sphinx

Sphinx is a rather mature documentation tool, being heavily used in the python
community, and written almost entirely in python. It is the tool used for
documenting a large number of open source projects, for example the 
[Linux Kernel](https://www.kernel.org/doc/html/latest/index.html),
[Python itself](https://docs.python.org/3/),
[Blender](https://docs.blender.org/manual/en/latest/) and many more

## Lets get started

Lets implement a documentation stack for automating our documentation workflow!

### Prereq
- python with virtualenv and pip
- git
- `virtualenv venv && source venv/bin/activate`
- `pip install sphinx`

### Round 1: Sphinx with Readthedocs

First off on creating a scalable documentation stack with sphinx is to get
sphinx up and running. In addition I will host the test project on readthedocs,
for demo purposes and because its very easy.

#### Setting up sphinx

**Key points:**
- Sphinx is based on the rst text format, but can be extended to use markdown
- Sphinx provides a nice wizard and some utitiles for building docs with make
  right off the bat

A good guide is already provided in the [readthedocs docs](https://docs.readthedocs.io/en/latest/intro/getting-started-with-sphinx.html).  TL;DR we do the following

```
$ mkdir docs && cd docs
$ sphinx-quickstart # and stick to defaults
$ make html
$ $BROWSER _builds/html/index.html
```

If the above commands succeeded, you should have very basic docs in your browser
now. Sphinx uses rst and many nifty things to bring home good documentation,
and you will use the web and [sphinx doc](http://www.sphinx-doc.org/) when
doing your actual documentation.

However there is a few key skills which is important in order to write scalable
documentation, which I need to talk about, and that is modularization and
generating docs from docstrings.

#### Modular Documentation

Okay so lets extend the index.rst file with another file. Lets say we have the
following folder structure

```
docs/
 | -- index.rst
 | -- api.rst
```

To include the extended documentation, we write the following in `index.rst`:

```
Documentation is Awesome!
=========================

.. toctree::
   :maxdepth: 1
   :caption: Table of Contents:

   api
```

This should include the extend.rst file

#### Generating documentation from docstrings

First we make sure we can include our python code by adding the following in
our conf.py (fill out the path to the code):
```
sys.path.insert(0, os.path.abspath('<path to code>'))
```
and make sure the `'sphinx.ext.autodoc'` extention is added to extentions in
conf.py. To write docstrings in a different format than traditional
reStructuredText (such as numpy below), include the `'sphinx.ext.napoleon'` extention aswell.

Write docstrings in the code with, for example, the [NumPy](http://www.sphinx-doc.org/en/1.5/ext/example_numpy.html#example-numpy)
style docstrings, and finally compile the documentation.

`$ make html`

Now check out the docs, and you should see the docstrings in the documentation!

#### ReadTheDocs

Deploying on [ReadTheDocs](https://readthedocs.org) is quite straight forward.
Just set up a new account (with github), go to [Dashboard](https://readthedocs.org/dashboard/)
and press "Import a Project".  Then select the repository with the sphinx
documentation and you should be flying

If youve come this far, you can look at my test deployment [here](https://docme.readthedocs.io)

### Round 2: Sphinx with gh-pages
Since we ultimately want the documentation on gh-pages, This next point will
take on how we do that.

### Round 3: Sphinx with submodules
### Round 4: Authentication with Jekyll auth and Heroku Dyno
### Round 5: Bringing it all together
