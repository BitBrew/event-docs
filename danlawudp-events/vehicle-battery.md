# Vehicle Battery

## Properties

- body (object)
  - footer: `90` (number) - Contains a checksum for the message contents.
  - message: (object) - Contains the contents of the event.
    - value: `5.538384437561035` (number)
    - eventCount: `1` (number) - The number of times this event occurred during the trip.
  - eventType: (object) - Contains the data for the event.
    - type: `BatteryEvent` (string) - Indicates a type for this event.
    - data: `CriticalBatteryWarning`(enum[string]) - Further information about the battery event.
      - Members:
        - `ReturnToNormalVoltage`
        - `LowBatteryInfo`
        - `LowBatteryWarning`
        - `CriticalBatteryWarning`
        - `LowChargingSystemConcernSet`
        - `HighChargingSystemConcernSet`
        - `LowChargingSystemConcernReset`
        - `HighChargingSystemConcernReset`
        - `ExcessiveDrainAlertSet`
        - `ExcessiveDrainAlertTripStartReset`
        - `ExcessiveDrainAlertReset`
        - `Unknown`
  - header (object) - UDP-specifc object containing meta-data about the event.
    - timestamp: `2016-02-05T10:36:31-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - latitude: `42.2793934` (number)
    - tripType: `Trip`(enum[string]) - Indicates a contextual type for this event.
      - Members
        - `IgnitionOff`
        - `Trip`
        - `Idling`
        - `Unknown`
    - vehicleProtocolId: `ISO15765_11_BIT_CAN`(enum[string]) - The type of protocol the device detected on the vehicle bus.
      - Members
        - `NoProtocol` - Would only appear if a vehicle were being towed. 
        - `J1850VPW`
        - `J1850PWM`
        - `ISO9141`
        - `ISO14230_FIVE_BAWD`
        - `ISO14230_FAST_INIT`
        - `ISO15765_11_BIT_CAN`
        - `ISO15765_29_BIT_CAN`
        - `J1939`
        - `J1708`
        - `Unknown`
    - longitude: `-83.72955975` (number)
    - messageType: `10` (number) - 
    - odo: `22` (number) - Vehicle odometer or device-calculated odometer.
    - tripNumber: `23`- A sequential number that increases after each trip. Resets after 65,536 trips.
    - fixQuality: `FixOk` (enum[string]) - The validity and accuracy of the GPS data.
      - Members
        - `FixOk` - 2D or 3D fix. Latitude and longitude are valid.
        - `StoredFix` - Latitude and longitude are readings from (up to) 5 seconds ago, because the device has not been able to get a GPS fix for 5 seconds.
        - `FixInvalid` - Latitude and longitude are invalid.
        - `Unknown` - The platform cannot decode the value.
    - messageLength: `6`(number) - Indicates the total bytes of the message, including the checksum.
  
## Example

```json
{
  "header": {...},
  "body": {
    "footer": 90,
    "message": {
      "value": 5.538384437561035,
      "eventCount": 1,
      "eventType": {
        "type": "BatteryEvent",
        "data": "CriticalBatteryWarning"
      },
      "type": "OBDPidAndVehicleBatteryEvent"
    },
    "header": {
      "latitude": 42.2793934,
      "tripType": "IgnitionOff",
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "timeStamp": "2016-08-19T18:51:19-04:00",
      "longitude": -83.72955975,
      "messageType": 7,
      "odo": 0,
      "tripNumber": 3,
      "fixQuality": "FixOk",
      "messageLength": 11,
    },
    "isError": false
  }
}
```
