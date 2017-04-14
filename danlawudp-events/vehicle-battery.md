# Vehicle Battery

## Properties

Currently unavailable

- data: `CriticalBatteryWarning`(enum[string])
  - Members:
    - ReturnToNormalVoltage
    - LowBatteryInfo
    - LowBatteryWarning
    - CriticalBatteryWarning
    - LowChargingSystemConcernSet
    - HighChargingSystemConcernSet
    - LowChargingSystemConcernReset
    - HighChargingSystemConcernReset
    - ExcessiveDrainAlertSet
    - ExcessiveDrainAlertTripStartReset
    - ExcessiveDrainAlertReset
    - Unknown

## Example

```json
{
  "header": {...},
  "body": {
    "footer": 90,
    "message": {
      "value": 5.538384437561035,
      "eventCount": 0,
      "eventType": {
        "type": "BatteryEvent",
        "data": "CriticalBatteryWarning"
      },
      "type": "OBDPidAndVehicleBatteryEvent"
    },
    "header": {
      "latitude": 0,
      "tripType": "IgnitionOff",
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "timeStamp": "2016-08-19T18:51:19-04:00",
      "longitude": 0,
      "messageType": 7,
      "odo": 0,
      "tripNumber": 3,
      "fixQuality": "FixInvalid",
      "messageLength": 11,
    },
    "isError": false
  }
}
```
