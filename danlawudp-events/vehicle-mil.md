# Vehicle MIL

## Properties

Currently unavailable

## Example

```json
{
  "header": {...},
  "body": {
    "message": {
      "milTime": 1000,
      "clrDistance": 0,
      "milStatus": true,
      "deviceTripTime": 6633,
      "dtcCount": 11,
      "deviceTripDistance": 8,
      "clrTime": 0,
      "milDistance": 1000,
      "type": "VehicleMILInfo"
    },
    "footer": 112,
    "header": {
      "timestamp": "2016-11-16T17:31:42-05:00",
      "latitude": 0,
      "tripType": "Trip",
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "longitude": 0,
      "messageType": 50,
      "odo": 8,
      "tripNumber": 33,
      "fixQuality": "FixInvalid",
      "messageLength": 19
    },
    "isError": false
  }
}
```
