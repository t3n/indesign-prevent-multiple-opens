# Prevent shared InDesign files from being edited by multiple users

This tool provides a way to prevent multiple users from editing the same InDesign file on a network or cloud share at the same time.

## Background

Adobe InDesign apparently does not generate IDLK lock files when working from a cloud drive, such as Creative Cloud, Dropbox, Synology Drive (AFP, NFS), etc. This means that multiple users could open the same shared file at the same time with no warning, and then overwrite each other's changes. See [this related support community discussion](https://community.adobe.com/t5/indesign-discussions/idlk-files-over-cloud-storage/td-p/11307839).

This script uses the official [InDesign scripting capabilities](https://helpx.adobe.com/indesign/using/scripting.html) to create a temporary .txt file when an InDesign file is opened, serving as an alternative locking file. The file is populated with the InDesign user's name (configured in `File -> User`).

When another user tries to open the same document and this .txt file exists, the second user will get a warning modal indicating the name of the user who has the document open, and then the document will be closed.  When the original locking user eventually closes the file, the .txt file is also removed and the file again becomes available for other users to edit.

For the locking to work, this script must be installed one time on every device that will be running InDesign and accessing shared files.

## Installation

To install, place the .jsx script in this repository inside a `Startup Scripts` directory (which may need to be created) under the Adobe InDesign main `Scripts` directory, make sure the user's name is set in `File -> User` and then completely restart InDesign. Repeat this process on every device that will be accessing shared files.

### Details

There are several ways to access the Scripts directory. You can usually find it in one of these locations:

* On Mac, /Users/`<User>`/Library/Preferences/Adobe Indesign/`<version>`/`<language|e.g. de_DE>`/Scripts/
* On Windows, \Documents and Settings\\`<username>`\Application Data\Adobe\InDesign\\`<version>`\\`<language|e.g. de_DE>`\Scripts\

Alternatively, you can locate the folder following these steps:

1. Open InDesign
2. Visit `Window -> Utilities -> Scripts`
3. Right click on “User” and select reveal in Finder/Explorer to open the Scripts folder

After you have located the directory, create a new folder called `Startup Scripts` (exact case and spacing and then copy/drag the [prevent-multiple-opens.jsx](prevent-multiple-opens.jsx) file into that folder. Then, restart InDesign.

## Special thanks
This script is heavily based on [Kasyan Servetsky's Script](http://kasyan.ho.ua/indesign/event_scripts/warn_about_docs_open_on_dropbox/warn_about_docs_open_on_dropbox.html) for InDesign files handled through Dropbox.
