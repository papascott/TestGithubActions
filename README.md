# electricDrummerDev

These are beta packages of Electric Drummer built by <a href="https://github.com/scotthansonde/">Scott Hanson</a> (using <a href="https://www.electron.build/">electron-builder</a>) for Linux, Windows and Mac 

### 17 Jan 2022 Version 0.4.5

No changes from 0.4.4 except bumping the version number. Now packaging rpm instead of snap. Builder now uploads packages to S3.

<b>Linux:</b> <a href="https://s3.amazonaws.com/ed-dist.scotthanson.de/electricDrummer_0.4.5_amd64.deb">electricDrummer_0.4.5_amd64.deb</a> and <a href="https://s3.amazonaws.com/ed-dist.scotthanson.de/electricDrummer-0.4.5.x86_64.rpm">electricDrummer-0.4.5.x86_64.rpm</a> 

<b>Windows:</b> <a href="https://s3.amazonaws.com/ed-dist.scotthanson.de/Electric+Drummer+Setup+0.4.5.exe">Electric Drummer Setup 0.4.5.exe</a>

<b>Mac:</b> <a href="https://s3.amazonaws.com/ed-dist.scotthanson.de/Electric+Drummer-0.4.5.dmg">Electric Drummer-0.4.5.dmg</a>

### 15 Jan 2022 Proper packages for Windows and Linux

<b>Linux</b>: <a href="https://s3.amazonaws.com/publicfolder.papascott.de/electric-drummer_0.4.4_amd64.deb">electric-drummer_0.4.4_amd64.deb</a> (for Ubuntu)

- This will make entries in the window manager so you don't have to start from the terminal 

- If you installed the test package from 12 Jan, uninstall it first with `sudo apt remove electricdrummer`

- Download the file, then install with `sudo apt install ./electric-drummer_0.4.4_amd64.deb`

- For other distributions there is a <a href="https://en.wikipedia.org/wiki/Snap_(package_manager)">snap</a> package that we have not tested: <a href="https://s3.amazonaws.com/publicfolder.papascott.de/electric-drummer_0.4.4_amd64.snap">electric-drummer_0.4.4_amd64.snap</a>

<b>Windows:</b> <a href="https://s3.amazonaws.com/publicfolder.papascott.de/Electric+Drummer+Setup+0.4.4.exe">Electric Drummer Setup 0.4.4.exe</a>

- This is a one-click installer. It will make an entry in your start menu and put an alias on your desktop to start the program.

- The data directory is in your user folder under AppData\Roaming\electric-drummer\data (AppData is a hidden folder)

<b>Mac: </b><a href="https://s3.amazonaws.com/publicfolder.papascott.de/Electric+Drummer-0.4.4.dmg">Electric Drummer-0.4.4.dmg</a>

### Setup the repository to build packages with <a href="https://www.electron.build/">electron-builder</a>

electron-builder is a third-party "complete solution to package and build a ready for distribution Electron app for MacOS, Windows and Linux"

- Install electron-builder globally `npm install -g electron-builder`

- Some fields in package.json need to be added or changed

  - `"name": "electric-drummer",` Linux wants all lower case

  - `"author": "Dave Winer <dave.winer@gmail.com>",`

  - `"description": "A multi-tab outliner that runs as a web app and as a desktop app",`

  - `"homepage": "http://docserver.scripting.com/drummer/electricDrummer.opml",`

- Windows wants a png icon at least 256x256. We converted drummer.icns to a png and called it <a href="https://s3.amazonaws.com/publicfolder.papascott.de/drummer512.png">drummer512.png</a>

- Add a <a href="https://gist.github.com/scotthansonde/a278ee35a96a48d0b1980f3d1c4df008">electron-builder.json</a> file for the configuration

To build for all platforms run `electron-builder -lwm` (<i>l</i>inux, <i>w</i>indows, <i>m</i>ac) or i.e. for Linux only with `electron-builder -l`

This works for Scott on his Intel MacBook Pro with MacOS Monterey 12.1 and nodejs v14.17.5

### 13 Jan 2022 Now also a test binary for Windows

Download from https://s3.amazonaws.com/publicfolder.papascott.de/Electric+Drummer+0.4.4.exe.zip

This is a "portable binary", extract the zip anywhere and double-click to run

The data directory is in your user folder under AppData\Roaming\electricDrummer\data (AppData is a hidden folder)

### 12 Jan 2022  First test package of <a href="http://docserver.scripting.com/drummer/electricDrummer.opml">Electric Drummer</a> than runs on Linux (tested on Ubuntu 20.04.2)

- Download the package from https://s3.amazonaws.com/publicfolder.papascott.de/electricdrummer_0.4.4_amd64.deb 

- In the terminal `sudo apt install ./electricdrummer_0.4.4_amd64.deb`

- In the terminal run <s>`electricDrummer`</s> `electricdrummer`

### Steps to build a deb package for Electric Drummer using electron-packager<br /> (tested on Mac and Linux server)

- On a Mac, the <a href="https://github.com/electron-userland/electron-installer-debian#requirements">deb packager</a> needs two command line tools: dpkg and fakeroot

  - The easiest way to install these is with <a href="https://brew.sh/">homebrew</a>

  - When homebrew is installed, then `brew install fakeroot dpkg` 

  - On Ubtuntu Linux (server or desktop) these commands should already be installed

- git clone the electric drummer repository

- Add a description field to package.json, the deb packager needs it

- `npx electron-packager . "electricDrummer" --platform=linux --arch=x64 --overwrite --icon=drummer.icns --electron-version=7.1.10`

  - npx lets us run npm packages without installing them

  - Set the appname to match "name" in package.json, the deb packager seems to be fussy about the name

  - Only build x64 arch to save time

- `npx electron-installer-debian --src electricDrummer-linux-x64 --dest Packages --arch amd64`

  - Set --dest to whereever the deb package should be saved

