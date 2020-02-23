# translator for the wallpanel android app
## decription
Wallpanel is a fantastic open source android app to show the Node-RED dashboard on any android device in kiosk mode. In addition it comes with mqtt support to read sensor data depending of the capabilities of your device and the ability to receive commnads
for more information you find the project here (https://thanksmister.com/wallpanel-android/)

## limitations
- **wallpanel** do not offer LWT support jet. So detection of $state is verry difficult epecially when your android device is not offering sensor data to detect a timeout. Use the $sate watchdog to emulate LWT
- **wallpanel** do not offer signal strength readings (WiFi)
- **no data conversion** Data conversion (i.e. voltage in %). Example can be found in the gerneric translator

## homie features
- `$name` *string* Name of the device
- `battery` *integer* Status of the battery in %
- `$localip` *string* the dashboard the wallpanel is pointing at. *this is not the ip of the android device!*

## extended features
- `charging` *boolean* indicator if the battery is charging
- `acPlugged` *boolean* indicator if the device is plugged it ac power (?)
- `usbPlugged` *boolean* indicator if the device is plugged into usb (?)
- `screenOn` *boolean* state of the screen (you can use a camera based motion detection, great!)
- `screenBrightness` *integer* current brightness of the screen
- `motion` *boolean* state of the motion sensor