<img src="https://i.ibb.co/QDfhn7W/joker-banner.png" style="width: max(45%, 400px); margin: .5rem;">
A simple shell script to download comics from readcomiconline.li via automated browser input, which seems to be the only
working solution in 2024.

# Dependencies
* required: `wget` `xdotool` `img2pdf` `bc` `dialog` `firefox-esr`
* optional: `gnome-terminal` `google-chrome`
```
debian: sudo apt-get install -y git wget xdotool img2pdf bc dialog firefox-esr
fedora: sudo dnf install git wget xdotool img2pdf bc dialog firefox-esr
arch: pacman -S git wget xdotool img2pdf bc dialog firefox-esr
```
# Usage

* clone this repo:
```
git clone https://github.com/tabletseeker/readcomic_dl -b main
```
* change directory:
```
cd readcomic_dl
```
* execute:
```
bash readcomic_dl
```
* make sure to adjust load_time and save_time to your liking as explained below, but also keep in mind that captchas are triggered if pages are loaded too quickly in series. The sweet spot is around 5-6 seconds for each.
* dialog already contains instructions for each window but you may also press the "Help" button, which can be toggled via TAB, for further information.
# Setup
* All prescribed changes are to be made in the readcomic_dl script file.

## File Locations
* this script uses the home directory as outputdir and ~/Downloads as workdir which can be
changed if necessary.
```
workdir="$HOME/Downloads/"
outputdir="$HOME/"
```
## Download Speed
* since all downloads are done via browser, delays have to be factored in for the
time needed to load all the images on a page and download them.
* depending on your internet speed you can choose the amount of seconds you would
like the script to wait for a page to load (load_time) and be downloaded (save_time).
* the script only downloads high quality variants, so make sure you adjust accordingly.
```
load_time=4
save_time=4
```
* readcomiconline has recently changed the way images load on the page, thus additional steps
  are necessary to ensure they are all captured. `scroll_num` determines the amount of bottom scroll events
  triggered by xdotool to ensure all images have been loaded. `scroll_delay` marks the delay between each scrolling event.
```
scroll_num=3
scroll_delay=10000
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
browser="firefox"
```
after:
```
browser="google-chrome"
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
## Donations :heartpulse:
If you like my contributions please feel free to drop a coin.
- Bitcoin URL: bitcoin: bc1qjz2dqu4u5uhxcv43jqmlefgffe3hnfavcs8w90
- Bitcoin Address: bc1qjz2dqu4u5uhxcv43jqmlefgffe3hnfavcs8w90
