# Vehicle DTCs - Pending

## Properties

Currently unavailable

## Example

```json
{
  "header": {...},
  "body": {
    "message": {
      "type": "VehiclePendingDTCInfo",
      "dtcRecords": [
        "P3412",
        "C2745",
        "B0888",
        "P2222"
      ]
    },
    "footer": 229,
    "header": {
      "timestamp": "2016-11-29T14:47:58-05:00",
      "latitude": 0,
      "tripType": "Trip",
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "longitude": 0,
      "messageType": 51,
      "odo": 101928,
      "tripNumber": 38,
      "fixQuality": "FixInvalid",
      "messageLength": 10
    },
    "isError": false
  }
}
```
