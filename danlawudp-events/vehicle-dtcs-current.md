# Vehicle DTCs - Current

## Properties

Currently unavailable

## Example

```json
{
  "header": {...},
  "body": {
    "message": {
      "milStatus": true,
      "type": "VehicleCurrentDTCInfo",
      "dtcSpnOrPidRecords": [
        "P3412",
        "C2745",
        "B0888",
        "P2222"
      ]
    },
    "footer": 67,
    "header": {
      "timestamp": "2016-11-16T17:31:28-05:00",
      "latitude": 0,
      "tripType": "Trip",
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "longitude": 0,
      "messageType": 18,
      "odo": 8,
      "tripNumber": 33,
      "fixQuality": "FixInvalid",
      "messageLength": 15
    },
    "isError": false
  }
}
```
