# Angular With Electron

Building a native desktop application with Angular and Electron. The application creates an executable that can be run on Windows, Mac, Ubuntu and browser as web app.

# Step to configure Angular Electron app
- Check if `node and node pakage manager (npm)` is installed.
- Install latest Angular <br/>
  `npm install -g @angular\cli`
- Create new angular application <br/>
  `ng new AngularElectron`
- Install Electron
  `npm install --save-dev electron`

## Changes needed on the Angular application
- Create new js file `main.js` in the root. Include the below content.<br/>
  ```
  const { app, BrowserWindow } = require('electron')

  // Keep a global reference of the window object, if you don't, the window will
  // be closed automatically when the JavaScript object is garbage collected.
  let win

  function createWindow () {
    // Create the browser window.
    win = new BrowserWindow({ width: 800, height: 600 })

    // and load the index.html of the app.
    win.loadFile('dist/AngularElectron/index.html')

    // Open the DevTools.
    //win.webContents.openDevTools()

    // Emitted when the window is closed.
    win.on('closed', () => {
      // Dereference the window object, usually you would store windows
      // in an array if your app supports multi windows, this is the time
      // when you should delete the corresponding element.
      win = null
    })
  }

  // This method will be called when Electron has finished
  // initialization and is ready to create browser windows.
  // Some APIs can only be used after this event occurs.
  app.on('ready', createWindow)

  // Quit when all windows are closed.
  app.on('window-all-closed', () => {
    // On macOS it is common for applications and their menu bar
    // to stay active until the user quits explicitly with Cmd + Q
    if (process.platform !== 'darwin') {
      app.quit()
    }
  })

  app.on('activate', () => {
    // On macOS it's common to re-create a window in the app when the
    // dock icon is clicked and there are no other windows open.
    if (win === null) {
      createWindow()
    }
  })

  // In this file you can include the rest of your app's specific main process
  // code. You can also put them in separate files and require them here.
  ```
- Update the `index.html` file 
  `<base href="./">` to include a period.
- Update the `package.json` file to add new initializer file.<br/>
  After `version` include `"main": "main.js"`<br/>
  In `scripts` include new command `"electron": "ng build && electron ."`

This is it !!

Run `npm run electron` in the terminal to see the magic.
  


