# Real Time Disconnect

## Properties

Currently unavailable

## Example

```json
{
  "header": {...},
  "body": {
    "footer": 212,
    "message": {
      "vehicleOdometer": 0,
      "calculatedOdometer": 1667,
      "isKeyOn": false,
      "vin": "JM1BK343551221507",
      "vehicleLastKnownLoc": 0,
      "type": "RealTimeDisconnectEvent",
      "vehicleOdoAvailable": false
    },
    "header": {
      "timestamp": "2016-08-22T16:08:10-04:00",
      "latitude": 42.278709411621094,
      "tripType": "IgnitionOff",
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "longitude": -83.74756622314453,
      "messageType": 53,
      "odo": 1667,
      "tripNumber": 92,
      "fixQuality": "FixOk",
      "messageLength": 30
    },
    "isError": false
  }
}
```
