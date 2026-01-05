nikthefix 050126

This is early days test code to render LVGL via websocket to HTML Canvas using USB-Ethernet (cdc-ncm) @192.168.4.1
It should work on any esp32-p4 board with at least 16MB of flash and PSRAM >= 2MB plus a native USB2.x High Speed Type 'C' or Type 'A' with a suitable yet dubiousely usb spec breaking 'A' to 'A' adapter.

It renders the LVGL frame buffers to a webpage canvas and feeds back mouse activity to the LVGL indev driver.
It sets up a new isolated 'ethernet' via USB so it won't disrupt your existing LAN and of course doesn't need wifi.

It requires esp-idf v5.5.2 and uses LVGL 8.x compatible code for the test gui.

The windows ncm host driver is not installed automatically at the time of writing but linux should auto-install. Not tested with MacOS or Android yet.
Use the following procedure to install the correct driver in win 10/11:
After plugging in the dev board it should appear in the windows device manager as an unknown device ('other devices' with a yellow exclamation mark).
Right click on the device entry and select update driver >
Browse my computer for drivers > 
Let me pick from a list of available drivers on my computer > 
select Network adapters > 
choose Microsoft as the manufacturer, and finally pick UsbNcm Host Device from the models, confirming the installation.
Replug the device and head to 192.168.4.1
A powershell script is included to automate the driver install process if prefered (at your own risk).

If you wish to try alternative ui from Squareline Studio / Squareline Vision / EZstudio then match the project display px dimensions in globals.h

I think this could be really useful - perfect for wifi provisioning and configuration in general.
Also, because the wifi is left free it could make a great pc-espnow gateway and many other types of bridge.

It would be more efficient to use Emscripten to serve WebAssembly and have all the LVGL stuff run in the browser (I'll try that next) but this approach is maybe useful as all the business code is running on the esp32 - the html canvas is simply a dumb external screen with mouse / touch callback. Modify index.html to change page background colour and default canvas position offset. Modify favicon.ico to your taste. index.html and favicon.ico are embedded as binaries at compile time so no file system is needed for the partition.




All credit goes to:

chegewara: https://github.com/esp32-p4-excercises/usb-netif-advanced-example

and

danjulio:
https://github.com/danjulio/lv_port_esp32_web

and

https://github.com/Molorius/esp32-websocket


If this project stands at all then it stands on the shoulders of these 3 talented and generous contributors.

```


MIT License

Copyright (c) [2026] [nikthefix]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
