# Device Health

## Properties

Currently unavailable

## Example

```json
{
  "header": {...},
  "body": {
    "message": {
      "faultGroup": "Information",
      "faultInformation": {
        "primaryAndSecondaryErrorCount": 0,
        "type": "ConfigFailure",
        "temporaryErrorCount": 0
      },
      "faultRecoveryAction": "SafeMode",
      "faultId": 29,
      "type": "DeviceHealthEvent"
    },
    "footer": 102,
    "header": {
      "timestamp": "2016-11-18T16:14:34-05:00",
      "latitude": 0,
      "tripType": "IgnitionOff",
      "vehicleProtocolId": "NoProtocol",
      "longitude": 0,
      "messageType": 15,
      "odo": 10,
      "tripNumber": 35,
      "fixQuality": "FixInvalid",
      "messageLength": 6
    },
    "isError": false
  }
}
```
