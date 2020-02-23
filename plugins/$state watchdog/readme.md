# msg.state.$state watchdog
## decription
this function provides a timeOut function (watchdog) to emulate the LWT functionality
issueing $state="lost" if a device did not update in time. 
on every received msg.state.$state it resets the timer
if the timer runs out it issues `msg.state.$state="lost"` and a message to 
the extra filed `msg.state.resetReason`

you can find more about the [homie convention device lifecyle here](https://homieiot.github.io/specification/#device-lifecycle).

## how to use
- place it in the main plugin list if you like to have a watchdog for every device with the same timeout
- place it after a translator / data source if only some devices need a watchdog because they do not supprt mqtt LWT or similar techniques to detect offline devices and set the msg.state.$state correcty over the complete lifecycle.
- place diffent watchdogs in the aquisition area behind translators if you need **individual timeout durations**.
- edit the `timeout` variable in the code or
- send msg.state.interval to set individual timeout by message

## do do / issues
- have to find out if a clearTimeout / setTimeout on every message is the most efficient way.
- perhaps own code with one interval timer more efficient for a bigger number of devices

## homie features
- `$state` *string* current state of the device
- `interval` *integer* in sec 

## extended features
- `resetReason` *string* description that the device was flagged by the watchdog
