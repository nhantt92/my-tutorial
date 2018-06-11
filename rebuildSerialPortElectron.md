# Rebuild SerialPort for Electron

## Use electron-rebuild

### install NET FW

### install Node

### Install Windows-build-tools

	`npm install -g windows-build-tools`

### install node-gyp
	
	`npm install -g node-gyp`

### install electron

### Add electron-rebuild

	`npm install --save-dev electron-rebuild`

### Add Serialport 

	`npm install --save serialport`

	remove .node binary (serialport it was \node_modules\serialport\build\Realease\serialport.node)

	run electron-rebuild.cmd


		```
		main.js#
		const electron = require('electron')
		// Module to control application life.
		const app = electron.app
		// Module to create native browser window.
		const BrowserWindow = electron.BrowserWindow

		const path = require('path')
		const url = require('url')

		const serialport = require('serialport')
		const SerialPort = serialport.SerialPort
		const parsers = serialport.parsers

		// Keep a global reference of the window object, if you don't, the window will
		// be closed automatically when the JavaScript object is garbage collected.
		let mainWindow

		let port

		function createWindow () {
		  // Create the browser window.
		  mainWindow = new BrowserWindow({width: 800, height: 600})

		  // and load the index.html of the app.
		  mainWindow.loadURL(url.format({
		    pathname: path.join(__dirname, 'index.html'),
		    protocol: 'file:',
		    slashes: true
		  }))

		  // Open the DevTools.
		  mainWindow.webContents.openDevTools()

		  // Emitted when the window is closed.
		  mainWindow.on('closed', function () {
		    // Dereference the window object, usually you would store windows
		    // in an array if your app supports multi windows, this is the time
		    // when you should delete the corresponding element.
		    mainWindow = null
		  })

		  port = new SerialPort('COM1', {
		    baudrate: 115200,
		    parser: parsers.readline('\r\n')
		  })
		  port.on('open', function() {
		    console.log('Port open');
		  })
		  port.on('data', function(data) {
		    console.log(data);
		  })
		}

		// This method will be called when Electron has finished
		// initialization and is ready to create browser windows.
		// Some APIs can only be used after this event occurs.
		app.on('ready', createWindow)

		// Quit when all windows are closed.
		app.on('window-all-closed', function () {
		  // On OS X it is common for applications and their menu bar
		  // to stay active until the user quits explicitly with Cmd + Q
		  if (process.platform !== 'darwin') {
		    app.quit()
		  }
		})

		app.on('activate', function () {
		  // On OS X it's common to re-create a window in the app when the
		  // dock icon is clicked and there are no other windows open.
		  if (mainWindow === null) {
		    createWindow()
		  }
		})

		// In this file you can include the rest of your app's specific main process
		// code. You can also put them in separate files and require them here.
		```

		Link: https://bl.ocks.org/tumoxep/4e7023bf1931a8016dafd6b60ca60a08

## Use node-gyp

	1. npm install -g node-gyp

	2. npm install --global --production windows=build-tools (run cmd as Administrator)

	3. Use

		node-gyp configure

		node-gyp configure --msvs_version=2015

		node-gyp build

	4. Error : bingging

		create file bingding.gyp có nội dung sau:

			```{
			  "targets": [
			    {
			      "target_name": "binding",
			      "sources": [ "src/binding.cc" ]
			    }
			  ]
			}```

	https://github.com/nodejs/node-gyp#installation



		npm install serialport --build-from-source
		https://github.com/nodejs/node-gyp#installation

		npm rebuild serialport --build-from-sources


	Link: https://www.npmjs.com/package/serialport-win-fix

	https://www.npmjs.com/package/serialport-builds-electron