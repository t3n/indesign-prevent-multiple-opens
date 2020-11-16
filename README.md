# Prevent InDesign to open a document multiple times

## Background

Adobe InDesign 2021 has a strange misbehaviour, when working from a cloud drive, such as Dropbox, Synology Drive (AFP, NFS) etc. The wanted behaviour that a warning is displayed when a network user already opened a specific document and a second user wants to open this exact document is not working. 
We found out that it's very likely caused by a wrong handling of the generated IDLK (InDesign Lock) file.

This script creates a .txt file in the document root and fills it up with the Username which is configured in `File -> User`. When another user is trying to open the document and this txt file exists, the second user will get a warning modal.

## How to install

To install this script, follow these steps (on MacOS):

```
1. Clone this repository
2. Create the folder /Users/<user>/Library/Preferences/Adobe Indesign/Version 16.0/<language|e.g. de_DE>/Scripts/Startup Scripts
3. Place the .jsx Script into the Startup Scripts folder
```
If you don't paste it into the Startup Scripts folder, it will not work!

## Special thanks
This script is heavily based on [Kasyan Servetsky's Script](http://kasyan.ho.ua/indesign/event_scripts/warn_about_docs_open_on_dropbox/warn_about_docs_open_on_dropbox.html) for InDesign files handled through Dropbox.
