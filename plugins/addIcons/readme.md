# Add and format icons
- This node is configured by a json object. 
- All incoming data inside `msg.state`is inspected to the parent keys of this object. 
- The value contains an array of objects defining different icons and styles to be added.
- a html formatted string is added to `msg.state.[key+"Icon"]`
- the current version supports font awesome icons supported by the dashboard and material icons including the style and size [ToDo] property
- Sting values will be compared for a case sensitive match
- values will be compared `<=`. So arrange the objects in a increasing order.

## configuration object
- defining the keys to be triggered
```json
{
    "$state":[],
    "signal":[],
    "battery":[]
}
```
- to trigger on a the value "init" to get a font awsome icon plce ´fa´ at the beginning of the `icon` value
```json
{
    "value":"init",
    "icon":"fa fa-cog fa-spin"
}
```
for material icons you can use
```json
{
    "value":10,
    "icon":"perm_scan_wifi",
    "style":"color:#cc0000"
}
```

Example:

```javascript
var icons= {
    "$state":[
        {"value":"init","icon":"fa fa-cog fa-spin"},
        {"value":"ready","icon":"fa fa-spinner fa-spin"},
        {"value":"disconnected","icon":"fa fa-times"},
        {"value":"sleeping","icon":"fa fa-moon-o"},
        {"value":"lost","icon":"fa fa-question-circle"},
        {"value":"lostBroker","icon":"fa fa-exclamation-triangle"},
        {"value":"alert","icon":"fa fa-exclamation-triangle"}
    ],
    "signal":[
        {"value":10,"icon":"perm_scan_wifi","style":"color:#cc0000"},
        {"value":20,"icon":"wifi","style":"color:#cc3300"},
        {"value":30,"icon":"wifi","style":"color:#cc6600"},
        {"value":40,"icon":"wifi","style":"color:#cc9900"},
        {"value":50,"icon":"wifi","style":"color:#cccc00"},
        {"value":60,"icon":"wifi","style":"color:#99cc00"},
        {"value":70,"icon":"wifi","style":"color:#66cc00"},
        {"value":80,"icon":"wifi","style":"color:#33cc00"},
        {"value":100,"icon":"signal_wifi_4_bar","style":"color:#00cc00"},
    ],
    "battery":[
        {"value":10,"icon":"battery-alert","style":"color:#cc0000"},
        {"value":20,"icon":"battery_20"},
        {"value":30,"icon":"battery_30"},
        {"value":50,"icon":"battery_50"},
        {"value":60,"icon":"battery_60"},
        {"value":70,"icon":"battery_70"},
        {"value":80,"icon":"battery_80"},
        {"value":90,"icon":"battery_90"},
        {"value":100,"icon":"battery_full","style":"color:#00cc00"},
    ]
};
```