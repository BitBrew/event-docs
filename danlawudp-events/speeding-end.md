# Speeding Event End
This event provides summarization of a high or critical speeding event after the vehicle's speed has dropped below the configured trigger velocity.

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
    - duration: `158` (number) - Duration of speeding event in seconds.
    - distance: `5.300000190734863` (number) - Distance traveled during speeding event in kilometers.
    - peakSpeed: `124` (number) - The maximum speed reached during this event in KPH.
    - averageSpeed: `122` (number) - The average speed during this event in KPH.
  - header (object) - UDP-specifc object containing meta-data about the event.
    - timestamp: `2017-06-25T22:22:58-04:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - tripType: `Unknown` (enum[string]) - Indicates a contextual type for this event.
      - Members
        - `IgnitionOff`
        - `Trip`
        - `Idling`
        - `Unknown`
    - tripNumber: `327`- A sequential number that increases after each trip. Resets after 65,536 trips.
    - messageType: `3` (number) - A unique number that correlates to the type field in the body of the message.
    - messageLength: `24` (number) - Indicates the total bytes of the message, including the checksum.
    - latitude: `42.06966781616211` (number)
    - longitude: `-86.4334945678711` (number)
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
            "duration": 158,
            "distance": 5.300000190734863,
            "peakSpeed": 124,
            "averageSpeed": 122
        },
        "header": {
            "timestamp": "2017-06-25T22:22:58-04:00",
            "tripType": "Unknown",
            "tripNumber": 327,
            "messageType": 3,
            "messageLength": 24,
            "latitude": 42.06966781616211,
            "longitude": -86.4334945678711,
            "fixQuality": "FixOk",
            "vehicleProtocolId": "ISO15765_11_BIT_CAN",
            "odo": 6168
        }
    },
}
```
