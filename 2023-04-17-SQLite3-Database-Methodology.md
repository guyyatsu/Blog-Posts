---
layout: post
title: SQLite3 DB Implementation
tags: knowledge howto
category: programming

---

# Python3 SQLite3 Tutorial & Lab-93 Implementation
[SQLite](https://en.wikipedia.org/wiki/SQLite) is the most widespread object-relational data storage system, deployed as an embedded database among browsers, phones, and any other conceivable device that would implement such a system.
Written in the C Programming Language, SQLite is based on the open-sourced PostgreSQL system; sharing a syntax structure, but little else.
Notable differences being the fact that SQLite is a _serverless_ database while PostgreSQL uses a [client/server](https://en.wikipedia.org/wiki/Client%E2%80%93server_model) type structure, and that SQLite utilizes a _statically implicit_ typing paradigm.


# Perks of Using SQLite3
For the high-level power-user and the barely-capable newbie alike, SQLite offers myriad benefits over it's competitors by being a cross-platform, zero-config, filesystem based directory system that also adheres to industry standards by maintaining [ACID](https://en.wikipedia.org/wiki/ACID) compliance.

## Cross-Platform Filesystem-Based Portability
SQLite follows the [UNIX](https://en.wikipedia.org/wiki/Unix) [philosophy](https://en.wikipedia.org/wiki/Unix_philosophy) that [```Everything is a File```](https://en.wikipedia.org/wiki/Everything_is_a_file), and embodies that by branching off from the typical ```client/server``` model that _most_ database systems employ.
Because of SQLite's filesystem based object lifetime it is entirely independent of the host operating system; so long as the developer is capable of navigating the filesystem structure of their machine then they can host instances of the same ```.db ``` file from any operating system with the same behaviour across the board.


# [Lab-93 Database System](https://lab-93.guyyatsu.me/documentation/Lab93DatabaseSystem)
In an effort to unify the server sytem among it's disparate pieces a __*grand unified database*__ was envisioned to objectify the process behind the creation of the original lab database, and to rebuild and expand upon the original lab database.
That idea then became what is currently being called the ```Lab93DatabaseSystem``` on pip; but the name is in dire need of a change to make the namespace less confusing.


The package offers a simple command-line functionality suite for interfacing with the lab's current iteration of a database by acting as a glue repository for expanding the functionality of said database through standardized processes.

## Graphical Database Management
Version 0.0.2 of the program will include a graphical db management system written in tkinter, and aims to offer a simple panel for building and maintaining a database.

### Database Selection
Upon selecting the program a pop-up window will show prompting for either an absolute filepath or to select an appropriate file by navigating the filesystem graphically.

### Content Enumeration
After selecting a ```.db``` file the database manager will query said file for it's contents and meta-data helping to describe the architectural structure.
Individual tables in the file are represented as tabs; and the first row of each tab lists each of the tables headers as a column.
From here, each table is queried for the entirety of it's records line by line and displayed in order of each entries coresponding column header.
