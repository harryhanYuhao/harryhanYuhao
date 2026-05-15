---
date: '2026-05-15T09:09:50+01:00'
draft: false
title: 'Cheatsheet for Qt Build and Development'
tags: ["qt", "Software Development", "c++"]
TocOpen: false
hidemeta: false
comments: false
description: "Quick steps to create a blog with Github Pages, Hugo, and PaperMod. Prerequisite: simple command line, git."
disableHLJS: true # to disable highlightjs
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
UseHugoToc: true
---

## Build System

Qt projects can be build with many different build softwares.
Among them`qmake` is the official build system and one of the most popular.
This is a quick introduction to `qmake`.

`qmake` reads a project file `<project-name>.pro`, which defines the project and list its source files, headers, and dependencies. 
A dummy example of a `.pro` file is this

```pro
# add qt widgets module to dependencies
QT += widgets

CONFIG += c++17 console
CONFIG -= app_bundle

SOURCES += \
    main.cpp \
    window.cpp

HEADERS += \
    window.h

FORMS += \
    window.ui
```

It is recommended to build the project in the build directory

```
mkdir build
cd build 
qmake ../<project-name>.pro # qmake generated the Makefile
make # make clean to clean the build directory
```

## QT projects on Neovim, Clangd and LSP

For the LSP server clangd to successfuly parse the project, it needs to know the location of the header files and the compiler flags.
This can be achieved using a JSON compilation database, which records the headers and dependencies of the source files.

The easiest way to generate a JSON compilation database is to use [bear](https://github.com/rizsotto/bear).
After running `qmake`, run the following command in the build directory to generate the `compile_commands.json` file.
```
bear -- make
```

And now the LSP server shall work correctly.
