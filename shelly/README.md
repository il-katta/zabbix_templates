# Shelly Plug by HTTP

Zabbix template for monitoring Shelly devices via HTTP. Tested with Shelly Plus2PM, Shelly PlusPlugS, Shelly PlugS Gen3, and Shelly PM Mini Gen3.

Template file: [shelly_plug_by_http.yaml](shelly_plug_by_http.yaml)

## Requirements

No installation required on the devices. The Zabbix server or proxy must be able to reach the Shelly devices via HTTP.

## Macro Configuration

### Required macros

- **{$SHELLY_HOST}**: hostname or IP address of the Shelly device

### Optional macros

- **{$SHELLY_USER}**: username for authentication (default: `admin`)
- **{$SHELLY_PASS}**: device password (only required if configured on the device, otherwise can be left empty)
- **{$SHELLY_TYPE}**: component type to retrieve data from in the JSON response (default: `switch`)
- **{$SHELLY_SWITCH_ID}**: switch/cover ID in the device (default: `0`)
- **{$SHELLY_MQTT_ENABLED}**: set to `1` to enable MQTT connection state monitoring, `0` to disable (default: `0`)
- **{$SHELLY_WIFI_RSSI_WARN}**: minimum WiFi RSSI signal strength threshold in dBm (default: `-70`)

## Determining {$SHELLY_TYPE} and {$SHELLY_SWITCH_ID} values

Shelly APIs return different data structures depending on the device. To identify the correct values, run:

```bash
curl -sL http://<ip_address>/rpc/Shelly.GetStatus | jq
```

Example response:

```json
{
  "ble": {},
  "cloud": {
    "connected": false
  },
  "mqtt": {
    "connected": true
  },
  "switch:0": {
    "id": 0,
    "source": "init",
    "output": true,
    "apower": 0.3,
    "voltage": 232.8,
    "current": 0.083,
    "aenergy": {
      "total": 114990.334,
      "by_minute": [
        0.000,
        0.000,
        0.000
      ],
      "minute_ts": 1759941180
    }
  }
}
```

In this example, the key is `"switch:0"`, so:
- **{$SHELLY_TYPE}** = `switch`
- **{$SHELLY_SWITCH_ID}** = `0`
