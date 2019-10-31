# Steam - Only update this game when I launch it

![¯\_(ツ)_/¯](https://img.shields.io/badge/works-brightgreen "for me")

## [Inspiration](https://steamcommunity.com/discussions/forum/10/2949168687320233261)

Currently, the Steam windows app defaults all games to `Always keep this game up to date`. I prefer otherwise, there are so many games in the library that I don't normally care to keep up to date. Since I am a code person by trade, here is my solution.

## Requirements

* Windows
* Bash on Windows (or any other flavour)
* Basic Bash skills

This solution uses lxss, because I'm most familiar working with Linux.

## Overview

Each steam app (game) has its own config file. These are located under the `steamapps` directory where you install the games (eg, `D:/Steam/steamapps`). Here you will find an `.acf` file for each of the games you already installed.

In these file, there is an entry for `AutoUpdateBehavior` and the value associated to it.
* `0` = `Always keep this game up to date`
* `1` = `Only update this game when I launch it`
* I don't care about the other one

The following steps will go through each of these and update them to 1.

## Steps

```bash
# go to your steam install directory (if you have multiple, you'll need to do this for each)
cd /mnd/d/Steam/steamapps

# magic!
sed -i 's/\("AutoUpdateBehavior"\s*\)"."/\1"1"/' `find . -maxdepth 1 -type f -iname '*.acf'`

# verify that all values are "1"
grep -s 'AutoUpdateBehavior' *
```

## Caveat

This only works for games you already downloaded. Every game you download will have a new config file, which means you'll need to run this again.
