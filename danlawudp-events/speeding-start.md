# Speeding Event Start
This event provides notification of a high or critical speeding event after the configured trigger criteria have been met, but before the event is over, so some fields are not available.

## Attributes

- body (object)
  - footer: `253` (number) - Contains a checksum for the message contents.
  - message: (object) - Contains the contents of the event.
    - type: `OverSpeedingMessage` (string) - Indicates a type for this event.
    - overSpeedType: `HighSpeed` (enum[string]) - A more specific category for this event.
      - Members
        - `HighSpeed`
        - `CriticalSpeed`
        - `Unknown`
    - startTime: `2017-06-26T02:20:20Z` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event began.
    - initialLatitude: `42.04869079589844`(number)
    - initialLongitude: `-86.49169921875` (number)
    - startODO: `6163` (number) - Vehicle or device odometer reading at the beginning of the event.
    - duration: `0` (number) - Duration not yet available since the event is still in progress.
    - distance: `0` (number) - Distance traveled during speeding event in kilometers.
    - peakSpeed: `0` (number) - The maximum speed reached during this event is not yet available since the event is still in progress.
    - averageSpeed: `0` (number) - The average speed during this event is not yet available since the event is still in progress.
  - header (object) - UDP-specifc object containing meta-data about the event.
    - timestamp: `2017-06-25T22:22:58-04:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - tripType: `Unknown` (enum[string]) - Indicates a contextual type for this event.
      - Members
        - `IgnitionOff`
        - `Trip`
        - `Idling`
        - `Unknown`
    - tripNumber: `327`- A sequential number that increases after each trip. Resets after 65,536 trips.
    - messageType: `22` (number) - A unique number that correlates to the `type` field in the body of the message.
    - messageLength: `24` (number) - Indicates the total bytes of the message, including the checksum.
    - latitude: `42.04963302612305` (number)
    - longitude: `-86.49064636230469` (number)
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
    - odo: `6168` (number) - Vehicle odometer or device-calculated odometer.

## Example

```json
    "header": {...}
    "body": {
        "footer": 253,
        "message": {
            "type": "OverSpeedingMessage",
            "overSpeedType": "HighSpeed",
            "startTime": "2017-06-26T02:20:20Z",
            "initialLatitude": 42.04869079589844,
            "initialLongitude": -86.49169921875,
            "startODO": 6163,
            "duration": 0,
            "distance": 0,
            "peakSpeed": 0,
            "averageSpeed": 0
        },
        "header": {
            "timestamp": "2017-06-25T22:22:58-04:00",
            "tripType": "Unknown",
            "tripNumber": 327,
            "messageType": 22,
            "messageLength": 24,
            "latitude": 42.04963302612305,
            "longitude": -86.49064636230469,
            "fixQuality": "FixOk",
            "vehicleProtocolId": "ISO15765_11_BIT_CAN",
            "odo": 6168
        }
    },
}
```
