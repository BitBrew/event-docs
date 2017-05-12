# VIN Change
This event is generated when the Datalogger detects a change in VIN, which will occur after the device powered on by a trip start.

## Attributes

- body (object)
  - footer: `227` (number) - Contains a checksum for the message contents.
  - message: (object) - Contains the contents of the event.
    - type: `VINChangeEvent` - Indicates a type for this event.
    - oldVin: `1C16G05GV2B104942` - Previously stored Vehicle Identification Number.
    - newVin: `JM1BK343551221507`- Current Vehicle Identification Number.
  - header (object) - UDP-specifc object containing meta-data about the event.
    - timestamp: `2017-03-31T20:12:18-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - tripType: `IgnitionOff` (enum[string]) - Indicates a contextual type for this event.
      - Members
        - `IgnitionOff`
        - `Trip`
        - `Idling`
        - `Unknown`
    - tripNumber: `3`(number) - A sequential number that increases after each trip. Resets after 65,536 trips.
    - messageType: `17` (number) -
    - messageLength: `37` (number) - Indicates the total bytes of the message, including the checksum.
    - latitude: `42.279937744140625` (number)
    - longitude: `-83.74799346923828` (number)
    - fixQuality: `FixOk` (enum[string]) - The validity and accuracy of the GPS data.
      - Members
        - `FixOk` - 2D or 3D fix. Latitude and longitude are valid.
        - `StoredFix` - Latitude and longitude are readings from (up to) 5 seconds ago, because the device has not been able to get a GPS fix for 5 seconds.
        - `FixInvalid` - Latitude and longitude are invalid.
        - `Unknown` - The platform cannot decode the value.
    - vehicleProtocolId: `ISO15765_11_BIT_CAN` (enum[string]) - The type of protocol the device detected on the vehicle bus.
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
    - odo: `88` (number) - Vehicle odometer or device-calculated odometer.

## Example

```json
{
  "header": {...},
  "body": {
    "footer": 227,
    "message": {
      "type": "VINChangeEvent",
      "oldVin": "1C16G05GV2B104942",
      "newVin": "JM1BK343551221507"
    },
    "header": {
      "timeStamp": "2017-03-31T20:12:18-05:00",
      "tripType": "IgnitionOff",
      "tripNumber": 3,
      "messageType": 17,
      "messageLength": 37,
      "latitude": 42.279937744140625,
      "longitude": -83.74799346923828,
      "fixQuality": "FixOk",
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "odo": 88
    },
    "isError": false
  }
}
```
