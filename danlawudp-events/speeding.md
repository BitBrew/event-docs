# Speeding

## Attributes

- body (object)
  - footer: `7` (number) - Contains a checksum for the message contents.
  - message: (object) - Contains the contents of the event.
    - type: `OverSpeedingMessage` (string) - Indicates a type for this event.
    - startTime: `2017-08-19T22:51:10Z` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event began.
    - initialLongitude: `-83.73925018310547` (number)
    - initialLatitude: `42.31918716430664`(number)
    - startODO: `1625` (number) - Vehicle or device odometer reading at the beginning of the event.
    - duration: `1` (number) - Duration of speeding event in seconds.
    - distance: `1.3` (number) - Distance travelled during speeding event in kilometers.
    - overSpeedType: `Unknown` (enum[string]) - A more specific category for this event.
      - Members
        - `HighSpeed`
        - `CriticalSpeed`
        - `Unknown`
    - peakSpeed: `85` (number) - The maximum speed reached during this event in KPH.
    - averageSpeed: `82` (number) - The average speed during this event in KPH.
  - header (object) - UDP-specifc object containing meta-data about the event.
    - timestamp: `2017-08-19T18:51:19-04:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - tripType: `Trip` (enum[string]) - Indicates a contextual type for this event.
      - Members
        - `IgnitionOff`
        - `Trip`
        - `Idling`
        - `Unknown`
    - tripNumber: `91`- A sequential number that increases after each trip. Resets after 65,536 trips.
    - messageType: `22` (number) - 
    - messageLength: `24` (number) - Indicates the total bytes of the message, including the checksum.
    - latitude: `42.321903228759766` (number)
    - longitude: `-83.74046325683594` (number)
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
    - odo: `1625` (number) - Vehicle odometer or device-calculated odometer.

## Example

```json
{
  "header": {...},
  "body": {
    "footer": 7,
    "message": {
      "type": "OverSpeedingMessage",
      "startTime": "2017-08-19T22:51:10Z",
      "initialLongitude": -83.73925018310547,
      "initialLatitude": 42.31918716430664,
      "startODO": 1625,
      "duration": 1,
      "distance": 1.3,
      "overSpeedType": "Unknown",
      "peakSpeed": 85,
      "averageSpeed": 82
    },
    "header": {
      "timestamp": "2017-08-19T18:51:19-04:00",
      "tripType": "Trip",
      "tripNumber": 91,
      "messageType": 22,
      "messageLength": 24,
      "latitude": 42.321903228759766,
      "longitude": -83.74046325683594,
      "fixQuality": "FixOk",
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "odo": 1625
    },
    "isError": false
  }
}
```
