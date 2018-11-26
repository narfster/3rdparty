# super build for boost and opencv linux

## Introduction

A cmake script to setup [boost](https://www.boost.org/) or [opencv](https://opencv.org/) on your system.

Yes it's just script, and yes it's yet another super build cmake script but what it does is no less then ***magic***!

## Description (aka what it does..)

- Downloads source release of opencv / boost from offcial repo
- Builds.
- Installs.
- simple to understand and modify.

## Requirements

This script is for programmers familiar with cmake and who need basic control over setup of these 3rd party libs.

* **git** you need it.
* **gcc** or a diffrent compiler you won't get far without one.
* **cmake 3.5.1** after all it is a cmake script.
## Usage

```
sudo git clone <this repo>   # clone this baby
cmake .                      # generate a makefile
sudo make boost              # make boost
sudo make opencv             # make opencv
```
***it's magic!***


## Licence 
It's FOSS!

