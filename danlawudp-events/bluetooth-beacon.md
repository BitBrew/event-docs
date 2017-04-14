# Bluetooth Beacon

## Properties

Currently unavailable

## Example

```json
{
  "header": {...},
  "body": {
    "footer": 206,
    "message": {
      "beaconInfo": [{
        "visibilityScore": 232,
        "bluetoothAddress": 4177060611,
        "type": "BeaconInfo"
      }],
      "type": "BluetoothBeaconMessage"
    },
    "header": {
      "timestamp": "2016-02-05T12:55:34-05:00",
      "latitude": 42.47832489013672,
      "tripType": "Trip",
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "longitude": -83.45087432861328,
      "messageType": 30,
      "odo": 45,
      "tripNumber": 26,
      "fixQuality": "FixOk",
      "messageLength": 24
    },
    "isError": false
  }
}
```
