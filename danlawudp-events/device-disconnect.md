# Device Disconnect

## Properties

Currently unavailable

## Example

```json
{
  "header": {...},
  "body": {
    "message": {
      "eventType": "Disconnect",
      "firmwareVersion": "07.2E",
      "odometer": 0,
      "keyOnOffDisconnect": "KeyOffDisconnect",
      "cfgVersion": "JHGDL13",
      "eventTime": "2016-12-29T10:46:58-05:00",
      "type": "ConnectDisconnectEvent",
      "odometerInfo": "VehicleOdometer"
    },
    "footer": 128,
    "header": {
      "timestamp": "2016-12-29T10:56:23-05:00",
      "latitude": 42.478084564208984,
      "tripType": "Trip",
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "longitude": -83.45092010498047,
      "messageType": 14,
      "odo": 0,
      "tripNumber": 2,
      "fixQuality": "FixInvalid",
      "messageLength": 32
    },
    "isError": false
  }
}
```
