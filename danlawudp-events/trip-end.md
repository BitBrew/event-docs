# Trip End

## Attributes

- body (object)
  - footer: `94` (number) - Contains a checksum for the message contents.
  - message: (object) - Contains the contents of the event.
    - type: `TripEndEvent` (string ) - Indicates a type for this event.
    - tripTime: `1158` (number) - 
    - distanceTravelled: `6.0` (number) -
    - cumulativeRunningTime: `113` (number) - Time the engine has been running since the device was connected in hours.
    - calculatedFuelConsumed: `0.28800000000000003` (number) - Amount of fuel consumed during the trip in gallons.
    - avgSpeed: `37` (number) - Average vehicle speed during the trip in KPH.
    - maxSpeed: `69` (number) - Maximum vehicle speed reached during the trip in KPH.
    - highSpeedEventCounts: `0` (number) - Number of high speed events during the trip.
    - highSpeedDuration: `0` (number) - Time spent in high speed events during the trip in seconds.
    - criticalSpeedEventCounts: `0` (number) - Number of critical speed events during the trip.
    - criticalSpeedDuration: `0` (number) - Time spent in critical speed events during the trip in seconds.
    - tripIdleTime: `586` (number) - Time the engine spent idling during the trip in seconds.
    - cumulativeIdleTime: `39` (number) - Time the engine has been idling since the device was connected in hours.
    - hardAcclCounts: 0` (number) - Number of hard acceleration events during the trip.
    - hardBreakingCounts: `0` (number) - Number of hard braking events during the trip.
    - consumedAir: `11868.81` (number) - Amount of air consumed dduring the trip in grams.
  - header (object) - UDP-specifc object containing meta-data about the event.
    - timestamp: `2017-08-22T16:08:10-04:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - tripType: `IgnitionOff`(enum[string]) - Indicates a contextual type for this event.
      - Members
        - `IgnitionOff`
        - `Trip`
        - `Idling`
        - `Unknown`
    - tripNumber: `92`- A sequential number that increases after each trip. Resets after 65,536 trips.
    - messageType: `53` (number) - 
    - messageLength: `30` (number) - Indicates the total bytes of the message, including the checksum.
    - latitude: `42.278709411621094` (number)
    - longitude: `-83.74756622314453` (number)
    - fixQuality: `FixOk` (enum[string]) - The validity and accuracy of the GPS data.
      - Members
        - `FixOk` - 2D or 3D fix. Latitude and longitude are valid.
        - `StoredFix` - Latitude and longitude are readings from (up to) 5 seconds ago, because the device has not been able to get a GPS fix for 5 seconds.
        - `FixInvalid` - Latitude and longitude are invalid.
        - `Unknown` - The platform cannot decode the value.
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
    - odo: `1667` (number) - Vehicle odometer or device-calculated odometer.

## Example

```json
{
  "header": {...},
  "body": {
    "footer": 94,
    "message": {
      "type": "TripEndEvent",
      "tripTime": 1158,
      "distanceTravelled": 6.0,
      "cumulativeRunningTime": 113,
      "calculatedFuelConsumed": 0.28800000000000003,
      "avgSpeed": 37,
      "maxSpeed": 69,
      "highSpeedEventCounts": 0,
      "highSpeedDuration": 0,
      "criticalSpeedEventCounts": 0,
      "criticalSpeedDuration": 0,
      "tripIdleTime": 586,
      "cumulativeIdleTime": 39,
      "hardAcclCounts": 0,
      "hardBreakingCounts": 0,
      "consumedAir": 11868.81
    },
    "header": {
      "timestamp": "2017-01-01T15:21:40-05:00",
      "latitude": 41.46466064453125,
      "tripType": "IgnitionOff",
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "longitude": -81.51720428466797,
      "messageType": 9,
      "odo": 3743,
      "tripNumber": 485,
      "fixQuality": "FixOk",
      "messageLength": 35
    },
    "isError": false
  }
}
```
