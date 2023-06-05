---
layout: post
title: Python3 Project Packaging
tags: knowledge howto
category: programming

---
# Packaging your software for ease of sharing.
Packaging a Python project using [```pip```](https://pypi.org/project/pip/) is an essential task for developers who seek to share their code with others or distribute it across different environments.  As pip is the standard package manager for Python, we will be using it to manage and
maintain all of the Lab-93 software tools written in it.

## Prerequisites
The pip repositories are maintained by the [```PyPi```](https://pypi.org) organization; who allow a simple process for uploading
packages to their servers, using pip as the front end.  You will need to create an account on their website and get an API key. 

In addition to proper PyPi credentials, you will also need to install the build toolchain for python.  This entails downloading
the ```build``` and ```twine``` modules.
```
python3 -m pip install --upgrade pip build twine
```


## Package Structure
Once you've finalized your script you have to enscapulate it in such a way so as to clearly demark the source from, say, the
documentation.  To do this, we have to structure our projects filesystem to reflect this.  Place the __init__.py file containing
your code within a directory of the name of your package inside of a directory labelled ```src/```.

Note that while you can
use dashes in the package name on PyPi, and thusly download it through pip using the dash character, Python itself __does not__
allow dashes in variable names.  So if any dash characters are used in the project name the actual package object has to use an
underscore instead.
```
package-project/
├── dist/
├── license
├── pyproject.toml
└── src/
    └── package_project/
        └── __init__.py
```


## Build Config
In order to build our project into a proper egg file we have to populate some fields within pyproject.toml.  This file describes
the metadata associated with the project for adhering to PyPi standards.  In it, we describe the project name, the build number,
the author(s) and their email(s), a sample description, interpreter version, license, and any web pages associated with the
project.

Every time the build module is invoked the build version must be increased; you __can not__ upload a modified version of a
previous edition.  Each build must be unique.

```
[build-system]
requires = ["setuptools>=61.0"]
build-backend = "setuptools.build_meta"

[project]
name = "package-project"
version = "0.0.1"
authors = [
  { name="Guyyatsu Hikikomori", email="hunter@guyyatsu.me" },
]
description = "A small example package"
readme = "readme.md"
requires-python = ">=3.7"
classifiers = [
    "Programming Language :: Python :: 3",
    "License :: OSI Approved :: MIT License",
    "Operating System :: OS Independent",
]

[project.urls]
"Homepage" = "https://gitserver/user/repository"
"Bug Tracker" = "https://gitserver/user/repository/issues"
```


## Licensing Considerations
In our example we are using the MIT License, however the GPLv3 also exists
and is the more attractive option for singleton programmers doing this in the
name of the game.  Simply copy and paste this snippet while updating the proper
year and author in the first line, and save as the file ```license``` in your
projects root directory.

```
Copyright (c)  2023  Guyyatsu Hikikomori

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```


## Building & Uploading
Now that overhead considerations are out of the way we can begin to build our
project and upload it to PyPi.  With ```build``` and ```twine``` we can automate
the process with a script:
```
python3 -m build && python3 -m twine upload dist/*
```

After a series of text-falling and a successful build the resulting binaries will be
uploaded, and you will be prompted for your PyPi username.
```
Uploading distributions to https://test.pypi.org/legacy/
Enter your username: __token__
```
Do not enter your actual username; instead enter ```__token__```; and when prompted for
the password enter the API key obtained as a pre-requisite.
