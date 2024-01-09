<img src="https://i.ibb.co/QDfhn7W/joker-banner.png" style="width: max(45%, 400px); margin: .5rem;">
A simple shell script to download comics from readcomiconline.li via automated browser input, which seems to be the only
working solution in 2024.

# Dependencies
* required: `wget` `xdotool` `img2pdf` `bc` `dialog` `firefox`
* optional: `gnome-terminal` `google-chrome`
```
debian: sudo apt-get install -y wget xdotool graphicsmagick bc dialog
fedora: sudo dnf install wget xdotool graphicsmagick bc dialog
arch: pacman -S wget xdotool graphicsmagick bc dialog
```
# Usage

* clone this repo:
```
cd $HOME
git clone https://github.com/tabletseeker/readcomic_dl -b main
```
* enter dir & execute:
```
cd readcomic_dl
chmod +x *
./readcomic_dl
```
* dialog already contains instructions for each window but you may also press the "Help" button, which can be toggled via TAB, for further information.
# Setup
* All prescribed changes are to be made in the readcomic_dl script file.

## File Locations
* this script uses the following default locations which can be
changed if necessary.
* if you clone into the home directory no changes are needed.
```
autosave="$HOME/readcomic_dl/autosave"
workdir="$HOME/Downloads/"
outputdir="$HOME/"
```
## Download Speed
* since all downloads are done via browser, delays have to be factored in for the
time needed to load all the images on a page and download them.
* depending on your internet speed you can choose the amount of seconds you would
like the script to wait for a page to load (load_time) and be downloaded (save_time).
* the script only downloads hiqh quality variants, so make sure you adjust accordingly.
```
load_time=6
save_time=4
```

## Terminal Requirements
 * dialog needs a minimum terminal geometry of 75x36 (RowsxColumns)
 * you can either manually resize your terminal window or simply
 create a .desktop file for easier access and automation.
```
[Desktop Entry]
Name=readcomic
Exec=gnome-terminal --geometry=75x36 -- /home/user/readcomic_dl/readcomic_dl
Terminal=false
Type=Application
```
## URL Requirements
* this script uses any given main page link to create a list of all available
comics which you can freely choose from by individual selection or the creation of a download range.
* the following would be an acceptable main page URL:
```
https://readcomiconline.li/Comic/Invincible
```
* this on the other hand would not be:
```
https://readcomiconline.li/Comic/Invincible/Issue-117?id=32948
```
## Web Browser 
* this script requires either Firefox or Chrome to automatically download
via xdotool.
* by default Firefox is being used. The following needs to be changed
in order to switch to Chrome (which needs to be installed):

before:
```
"$autosave" -b firefox
```
after:
```
"$autosave" -b google-chrome
```
## Dialog
* .dialogrc contains custom style settings which should make your dialog
use a black and white color scheme.
* the rc file is only copied if you don't already have one.
* if you prefer the default theme you can delete ~/.dialogrc
and create a standard one like so:
```
dialog --create-rc ~/.dialogrc
```
