### Desktop Appp
```
npm install --save-dev electron
```
```
npm install --save-dev electron-builder
```
index.html
```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>DesktopAngularElectron</title>
    <base href="./" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <link rel="icon" type="image/x-icon" href="favicon.ico" />
  </head>
  <body>
    <app-root></app-root>
  </body>
</html>
```
```
<base href="./" />
```
package.json
```
{
  "name": "desktop-angular-electron",
  "main": "main.js",
  "version": "0.0.1",
  "authors": "tharindu",
  "description": "desktop app",
  "scripts": {
    "ng": "ng",
    "start": "ng serve",
    "build": "ng build",
    "watch": "ng build --watch --configuration development",
    "test": "ng test",
    "serve:ssr:desktop_angular_electron": "node dist/desktop_angular_electron/server/server.mjs",
    "electron": "ng build --base-href ./ && electron .",
    "dist": "ng build --base-href ./ && electron-builder"
  },
  "private": true,
  "dependencies": {
    "@angular/animations": "^18.0.0",
    "@angular/common": "^18.0.0",
    "@angular/compiler": "^18.0.0",
    "@angular/core": "^18.0.0",
    "@angular/forms": "^18.0.0",
    "@angular/platform-browser": "^18.0.0",
    "@angular/platform-browser-dynamic": "^18.0.0",
    "@angular/platform-server": "^18.0.0",
    "@angular/router": "^18.0.0",
    "@angular/ssr": "^18.0.1",
    "express": "^4.18.2",
    "rxjs": "~7.8.0",
    "tslib": "^2.3.0",
    "zone.js": "~0.14.3"
  },
  "devDependencies": {
    "@angular-devkit/build-angular": "^18.0.1",
    "@angular/cli": "^18.0.1",
    "@angular/compiler-cli": "^18.0.0",
    "@types/express": "^4.17.17",
    "@types/jasmine": "~5.1.0",
    "@types/node": "^18.18.0",
    "electron": "^30.0.8",
    "jasmine-core": "~5.1.0",
    "karma": "~6.4.0",
    "karma-chrome-launcher": "~3.2.0",
    "karma-coverage": "~2.2.0",
    "karma-jasmine": "~5.1.0",
    "karma-jasmine-html-reporter": "~2.1.0",
    "typescript": "~5.4.2"
  },
  "build": {
    "appId": "software.cantrips",
    "productName": "SoftwareCantrips",
    "mac": {
      "category": "public.app-category.developer-tools"
    },
    "files": [
      "**/*",
      "dist/desktop_angular_electron/browser/**"
    ]
  }
}
```
```
"main": "main.js",
"version": "0.0.1",
"authors": "tharindu",
"description": "desktop app",
```
```
"build": {
    "appId": "software.cantrips",
    "productName": "SoftwareCantrips",
    "mac": {
      "category": "public.app-category.developer-tools"
    },
    "files": [
      "**/*",
      "dist/desktop_angular_electron/browser/**"
    ]
  }
```
main.js
```

const { app, BrowserWindow } = require('electron')
const url = require('url');
const path = require('path');
let mainWindow
function createWindow () {
  mainWindow = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      nodeIntegration: true
    }
  })
  mainWindow.loadURL(
    url.format({
      pathname: path.join(__dirname, `/dist/desktop_angular_electron/browser/index.html`),
      protocol: "file:",
      slashes: true
    })
  );
  // mainWindow.webContents.openDevTools()
  mainWindow.on('closed', function () {
    mainWindow = null
  })
}
app.on('ready', createWindow)
app.on('window-all-closed', function () {
  if (process.platform !== 'darwin') app.quit()
})
app.on('activate', function () {
  if (mainWindow === null) createWindow()
})
```
Run App
```
npm run electron
```
```
npm run dist
```