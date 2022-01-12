# Steps to build a deb package for Electric Drummer (either on Mac or a Linux server)

1 On a Mac, the <a href="https://github.com/electron-userland/electron-installer-debian#requirements">deb packager</a> needs two command line tools: dpkg and fakeroot

  The easiest way to install these is with <a href="https://brew.sh/">homebrew</a>

  When homebrew is installed, then `brew install fakeroot dpkg` 

1 git clone the electric drummer repository

1 Add a description field to package.json, the deb packager needs it

1 `npx electron-packager . "electricDrummer" --platform=linux --arch=x64 --overwrite --icon=drummer.icns --electron-version=7.1.10`

  npx lets us run npm packages without installing them

  Set the appname to match "name" in package.json, the deb packager seems to be fussy about the name

  Only build x64 arch to save time

1 `npx electron-installer-debian --src electricDrummer-linux-x64 --dest Packages --arch amd64`

  Set --dest to whereever the deb package should be saved

