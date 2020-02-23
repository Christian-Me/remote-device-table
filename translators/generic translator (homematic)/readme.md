# generic translator (here for Homematic devices)

This function node is a generic translator for data comming in as a msg object. As an example the converting data from the homematic in node to msg.state is performed.

## theory of operation

The remote device table originates in the [homie convention](https://homieiot.github.io) but can be relatively easyly adapted for other systems. If ever possible the data from other systems should be merged into the homie convention properties to keep the amount of columns in the table low and make it easy to be compared, sorted and filtered. But feel free to add additional proerties as you like. Some properties a essential and should not be changed

** required properties **
- **$topic** essential is a unique index. Unique in this case means unique for ALL remote devices. Otherwise you will get different devices merged into each other. `msg.state.$topic` will be copied into msg.topic to make it easier to access
- **$name** should be unique and will be inside one mqtt base topic but as every row is identified by $topic it could be edited.
- **$state** current or last known state of the device | string | ["ready", "lost", "init", "sleeping", "disconnected", "alert"

** special properties **

- **interval** If your device do not provide the inteval ime (on seconds) it could be expected to send updates you should set the fefault to an apropiate time. The `$state watchdog` uses this to set a individual timeout for each device. Set it to 0 when you do not expect regular updates.
 
## suggested / reserved properties

This properties are defined by the homie convention and should be used if possible!

property | description | type    | format 
-------- | ----------- | ------- | ------ 
$homie | The implemented Homie convention version | **string** | "4.0.0"
$name | the **unique** name of the device. This name is used to identify the device in the table. | string | "myDevice"
$state | current or last state of the device | string | ["ready", "lost", "init", "sleeping", "disconnected", "alert"]
$nodes	| Nodes the device exposes | array | comma seperated list
$extensions	| Supported extensions | array | comma seperated list
$implementation | An identifier for the Homie implementation | string | "esp8266"



defined by [**Legacy Firmware**](https://github.com/homieiot/convention/blob/develop/extensions/documents/homie_legacy_firmware_extension.md)

property | description | type    | format
-------- | ----------- | ------- | ------
$localip | IP of the device on the local network | string | "127.0.0.1"
$mac | Mac address of the device network interface | string | The format MUST be of the type `A1:B2:C3:D4:E5:F6`
name | Name of the firmware running on the device. | string | Allowed characters are the same as the device ID
version | Version of the firmware running on the device. | string | "1.0.0"


defined by [**Legacy Stats**](https://github.com/homieiot/convention/blob/develop/extensions/documents/homie_legacy_stats_extension.md)

property | description | type    | format
-------- | ----------- | ------- | ------
interval | Interval in seconds at which the device refreshes its `$stats/+` | integer | Positive greater 0
uptime | Time elapsed in seconds since the boot of the device | integer | seconds
signal | Signal strength | Integer | in %
cputemp | CPU Temperature | Float | in °C
cpuload | CPU Load in. Average of last $stats\interval including all CPUs | Integer | %. 
battery | Battery level. | Integer | in %
freeheap | Free heap. |	Positive Integer | in bytes
supply | Supply Voltage | Float | in V

