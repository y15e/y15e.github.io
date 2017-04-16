---
layout: post
title: "Install Flux"
---

(1) Clone the Flux repository.

```
$ git clone https://github.com/facebook/flux.git
```

(2) Build Flux.

```
$ cd flux
$ npm install
```

Then following error occurred because of python version.

```
npm WARN deprecated gulp-clean@0.3.1: use gulp-rimraf instead
npm WARN engine jest-cli@0.4.1: wanted: {"node":"0.8.x || 0.10.x"} (current: {"node":"0.12.2","npm":"2.8.3"})

> contextify@0.1.13 install /home/ywatanabe/work/flux/node_modules/jest-cli/node_modules/jsdom/node_modules/contextify
> node-gyp rebuild

gyp ERR! configure error
gyp ERR! stack Error: Python executable "python" is v3.4.3, which is not supported by gyp.
gyp ERR! stack You can pass the --python switch to point to Python >= v2.5.0 & < 3.0.0.
gyp ERR! stack     at failPythonVersion (/usr/lib/node_modules/npm/node_modules/node-gyp/lib/configure.js:108:14)
gyp ERR! stack     at /usr/lib/node_modules/npm/node_modules/node-gyp/lib/configure.js:97:9
gyp ERR! stack     at ChildProcess.exithandler (child_process.js:742:7)
gyp ERR! stack     at ChildProcess.emit (events.js:110:17)
gyp ERR! stack     at maybeClose (child_process.js:1015:16)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:1087:5)
gyp ERR! System Linux 4.0.1-1-ARCH
gyp ERR! command "node" "/usr/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /home/ywatanabe/work/flux/node_modules/jest-cli/node_modules/jsdom/node_modules/contextify
gyp ERR! node -v v0.12.2
gyp ERR! node-gyp -v v1.0.3
gyp ERR! not ok
npm ERR! Linux 4.0.1-1-ARCH
npm ERR! argv "/usr/bin/node" "/usr/bin/npm" "install"
npm ERR! node v0.12.2
npm ERR! npm  v2.8.3
npm ERR! code ELIFECYCLE

npm ERR! contextify@0.1.13 install: `node-gyp rebuild`
npm ERR! Exit status 1
npm ERR!
npm ERR! Failed at the contextify@0.1.13 install script 'node-gyp rebuild'.
npm ERR! This is most likely a problem with the contextify package,
npm ERR! not with npm itself.
npm ERR! Tell the author that this fails on your system:
npm ERR!     node-gyp rebuild
npm ERR! You can get their info via:
npm ERR!     npm owner ls contextify
npm ERR! There is likely additional logging output above.

npm ERR! Please include the following file with any support request:
npm ERR!     /home/ywatanabe/work/flux/npm-debug.log

```