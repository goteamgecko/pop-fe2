pop-fe2 is a python utility to create PS2Classic PKGs on Linux

WIP

For now it will only create PS2Classics for games where we have
all the assets defined in gamedb.py.
Please add icon0/pic0/pic1/snd0 links to any entries that are
uncommented in gamedb.py.

TODO:
add VMC support

IMPORTANT
=========
MAKE_NPDATA does not build on current Linux.
A patch for this is available at
https://github.com/Sorvigolova/make_npdata/pull/1 
but has not yet been  merged.
Use this repo for the time being:
https://github.com/masible/make_npdata/tree/wip/hadess/modern-linux


Usage
=====

To greate game.pkg from the iso stored in /path/to/game.iso :

$ ./pop-fe2.py --ps3-pkg=game.pkg /path/to/game.iso

You can also have pop-fe2 automatically use the game title from the database
as the name of the generated PKG by using the keyword 'title'

$ ./pop-fe2.py --ps3-pkg=title /path/to/game.iso

Or you can have it use the gameid as the name of the PKG using 'gameid'

$ ./pop-fe2.py --ps3-pkg=gameid /path/to/game.iso

By default pop-fe2 will create the PKG in the current directory.
You can also specify an alternative directory where the PKG should be created in
using --output-directory

$ ./pop-fe2.py --ps3-pkg=gameid --output-directory=/path/to/my/pkgs/ /path/to/game.iso


Batch processing is possible with some simple shellscripting.
For example to scan /path/to/my/isos for all ISO files and then generate a PKG
for each one of them, using the detected name of the game as the PKG filename
and writing them all to /path/to/my/pkgs  you can use something like:

$ find /path/to/my/isos | egrep ".iso$" | while read ISO; do ./pop-fe2.py --ps3-pkg=title --output-directory=/path/to/my/pkgs ${ISO}; done

Installation
============

```console
# Make sure your system has the following packages installed:
# git python3 libsndfile ffmpeg make cmake
# Clone all submodules
git submodule update --init --recursive
# Build required tools
make
# Install python requirements
pip3 install -r requirements.txt 
```
