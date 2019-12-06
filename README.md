# Binary patches for the rM

## Version 2.0.1.1
Those are features that I find useful/wanted for me to have. If someone else would like to try them, they are welcome.


## Disclaimer
*The files are offered without any warranty and you will be violating the reMarkable SA EULA by using them.
There may be bugs, you may loose data, your device may crash, etc.*

*The only guarantee is, that there is no ill intended code*

## Demo

![Screenshot1](docs/images/screenshot_bookmarks.png)
![Screenshot1](docs/images/screenshot_2011_numpad.png)
![Screenshot1](docs/images/screenshot_share.png)

## Changes

### patch_204
- add a toggle for swipe enable/disable

### patch_203
- change GoToPage icon to current/number of pages
- (bugfix) keyboard losing focus on bookmark edit (scroll disabled and may impact file exporting)
- do not display current page in the footer (goto page icon)
- fix: do not write on toc dialog

### patch_202
- add naming of bookmarks (press and hold the bookmark in the list)
- removed the close button
- toggle wifi button in the share menu (for easy on/off)

### patch_201
- gotopage (custom numpad input) 
- bookmark for the last page (go to last page)
- (bugfix) go to bookmarked folder in list mode
- Bookmarks (persistent, saved beside the original file with .bookm extension)
- jump forth and back (toc, goto page or bookmark)
- UI button size reduced by 16% (in order to pack more buttons) + some alignment issues
- show always the first page (cover) in Overview
- remove the thumbnails in listview
- reduce the height of the items in listview
- toc button
- scroll by a whole page in toc and listview
- (bugfix) do not reset the table of contents everytime it is shown

## Known issues
- bookmark position stays the same in landscape mode
- numpad does not validate the input (0 = first page, > pagecount = last page)
- listview scrolling is buggy
- had to remove the tooltips / tutorial
- dialog for filename / mesage body no longer scrollable

## Nice to have
- change the default tool on document create (i prefer the fineliner, thickness 1)
- fix the selection box dimensions (vertical or horizonatl straight lines are hard to manage)
- fix palm rejection timeout (cannot swipe pages, button input ignored, for 1-2 seconds after raising the pen)

## Things that I would like to do, but are hard
- pdf link navigation
- djvu support

# Installation
on the device (Rm->About->Copyright->General Information) write down, remember the password shown


## Linux
You got this


## Windows 10
open a command line prompt (Win-R, type cmd, enter)
ssh root@10.11.99.1 (type the password)
or install Putty and enter 10.11.99.1 as address and root for username
paste the automagic line

## macOS
open Spotlight (Cmd-Space) type Terminal, enter
ssh root@10.11.99.1 (type the password)
paste the automagic line

# Automagic
paste the following and press enter (replace _01 with _02 etc to use a different patch):
```
sh -c "$(wget https://raw.githubusercontent.com/ddvk/remarkable-hacks/master/patch.sh -O-)" _ patch_204
```
you will see a bunch of log messages, the app will start, play with it but press **CTRL-C** to stop it when done (DON'T LEAVE IT JUST RUNNING) and follow the instructions (i.e make it permanent or just start the stock one). 

### Notes
patches are cumulative (the last one contains all previous changes and gets updated with bugfixes)
a patch can be applied more than once, it's more of a snapshot really, you can go back to a previous version


# NB WARNING
Always clear the qml cache before switching/running versions manually (the script already does that). Failing to do so will result in a crash

## Making it permanent

After making sure everything is ok (i.e. no crashes) if you want to make it permanent (until the next sw update), you can replace the original, before running the original or rebooting (make sure you read the WARNING above)
```
#if you ran a different version
rm -fr .cache/remarkable/xochitl/qmlcache/*

cp xochitl.patched /usr/bin/xochitl
systemctl start xochitl
```


## Revert in case things go terribly wrong
ssh
```
systemctl stop xochitl
rm -fr .cache/remarkable/xochitl/qmlcache/*
cp xochitl.2011 /usr/bin/xochitl
systemctl start xochitl
```
