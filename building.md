# Building Mac electron apps (like Electric Drummer) for Linux and Windows

These are my instructions for building electron apps for Mac (like those developed by <a href="https://github.com/scripting">Dave Winer</a>) for Linux and Windows. As with most things, there is "more than one way to do it", but this worked for me.

For now I am only building zip files of the app, not packages that can be properly installed  in Linux and Windows.

I've tested this with the <a href="http://docserver.scripting.com/drummer/electricDrummer.opml">Electric Drummer</a> and <a href="http://this.how/publicFolder/">Public Folde</a>r apps. I work on a Mac with MacOS 12.3 (Monterey) and Node.js 16 (v16.14.0).  

### electron-builder

There are several alternative tools for building electron apps (including <a href="https://github.com/electron/electron-packager">electron-packager</a>, <a href="https://www.electronforge.io/">electron-forge</a>, <a href="https://www.electron.build/">electron-builder</a>). I found electron-builder to be the easiest and have the most options for building multi-platform apps.


Install the latest electron-builder globally with `npm install -g electron-builder`


### Configuration

electron-builder can be <a href="https://www.electron.build/configuration/configuration">configured</a> within package.json (in a 'build' key) or a separate file. I chose to use an electron-builder.json file.

My minimal electron-builder.json (for Public Folder)

```
{
"electronVersion": "7.1.10",
"directories": {
"buildResources": "."
},
"mac": {
"target": "zip",
"identity": null,
"icon": "bowlingBall.icns"
},
"win": {
"target": "zip",
"icon": "bowlingBall.png"
},
"linux": {
"target": "zip"
}
}
```

