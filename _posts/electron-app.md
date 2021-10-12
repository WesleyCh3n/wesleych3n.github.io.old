# Create electron app

```bat
npm init
npm install --save-dev electron
```

add following to `package.json`

```json
{
  "scripts": {
    "start": "electron ."
  }
}
```
and start
```
npm start
```
Then get error, XD

`main.js`
```javascript
// Modules to control application life and create native browser window
const { app, BrowserWindow } = require('electron')
const path = require('path')

function createWindow () {
  // Create the browser window.
  const mainWindow = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      preload: path.join(__dirname, 'preload.js')
    }
  })

  // and load the index.html of the app.
  mainWindow.loadFile('index.html')

  // Open the DevTools.
  // mainWindow.webContents.openDevTools()
}

// This method will be called when Electron has finished
// initialization and is ready to create browser windows.
// Some APIs can only be used after this event occurs.
app.whenReady().then(() => {
  createWindow()

  app.on('activate', function () {
    // On macOS it's common to re-create a window in the app when the
    // dock icon is clicked and there are no other windows open.
    if (BrowserWindow.getAllWindows().length === 0) createWindow()
  })
})

// Quit when all windows are closed, except on macOS. There, it's common
// for applications and their menu bar to stay active until the user quits
// explicitly with Cmd + Q.
app.on('window-all-closed', function () {
  if (process.platform !== 'darwin') app.quit()
})

// In this file you can include the rest of your app's specific main process
// code. You can also put them in separate files and require them here.

```

`preload.js`
```javascript
// preload.js

// All of the Node.js APIs are available in the preload process.
// It has the same sandbox as a Chrome extension.
window.addEventListener('DOMContentLoaded', () => {
  const replaceText = (selector, text) => {
    const element = document.getElementById(selector)
    if (element) element.innerText = text
  }

  for (const dependency of ['chrome', 'node', 'electron']) {
    replaceText(`${dependency}-version`, process.versions[dependency])
  }
})
```

`index.html`
```html
<!--index.html-->

<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <!-- https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP -->
    <meta http-equiv="Content-Security-Policy" content="default-src 'self'; script-src 'self'">
    <meta http-equiv="X-Content-Security-Policy" content="default-src 'self'; script-src 'self'">
    <title>Hello World!</title>
  </head>
  <body>
    <h1>Hello World!</h1>
    We are using Node.js <span id="node-version"></span>,
    Chromium <span id="chrome-version"></span>,
    and Electron <span id="electron-version"></span>.

    <!-- You can also require other files to run in this process -->
    <script src="./renderer.js"></script>
  </body>
</html>
```

---

# Package and distribute your application

- electron-forge
```bat
npm install --save-dev @electron-forge/cli
npx electron-forge import
npm run make
```

- electron-builder
```bat
npm i -D electron-builder
```

`build.js`
```javascript
const path = require('path');
const builder = require('electron-builder');

builder.build({

    projectDir: path.resolve(__dirname),  // 專案路徑

    win: ['nsis', 'portable'],  // nsis . portable
    config: {
        "appId": "com.wesleych3n.electron.app",
        "productName": "App Name", // 應用程式名稱 ( 顯示在應用程式與功能 )
        "directories": {
            "output": "build/win"
        },
        "win": {
            "icon": path.resolve(__dirname, 'logo.png'),
        }
    },
})
    .then(
        data => console.log(data),
        err => console.error(err)
    );
```

```bat
node ./build.js
```

---

# ffi-napi

install ffi-napi
```bash
npm i ffi-napi
```

in `main.js`
```javascript
// load ffi module
const ffi = require('ffi-napi')
const path = require('path')

// Test ffi-napi
const libpath = path.join(__dirname, '../myclib/myclib.dll')
var myclib = ffi.Library(libpath, {
  'fooGetCpuTemp': ['double', []],
  'fooSetMBFunc': ['bool', ['int', 'int']]
})
console.log(myclib.fooGetCpuTemp())
console.log(myclib.fooSetMBFunc(2,4))
console.log(myclib.fooSetMBFunc(10,10))
```
