# Idling

## Attributes
- body: (object)
  - footer: `5` (number) - Contains a checksum for the message contents.
  - message: (object) - Contains the contents of the event.
    - type: `IdlingMessage` (string) - Indicates a type for this event.
    - startTime: `2017-08-20T17:27:50Z` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event began.
    - duration: `566` (number) - The duration of the idling event in seconds.
  - header (object) - UDP-specifc object containing meta-data about the event.
    - timestamp: `2017-08-20T13:37:18-04:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - tripType: `IgnitionOff`(enum[string]) - Indicates a contextual type for this event.
      - Members
        - `IgnitionOff`
        - `Trip`
        - `Idling`
        - `Unknown`
    - tripNumber: `21`- A sequential number that increases after each trip. Resets after 65,536 trips.
    - messageType: `6` (number) - 
    - messageLength: `7` (number) - Indicates the total bytes of the message, including the checksum.
    - latitude: `42.299320220947266` (number)
    - longitude: `-85.19763946533203` (number)
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
    - odo: `190` (number) - Vehicle odometer or device-calculated odometer.

## Example

```json
{
  "header": {...},
  "body": {
    "footer": 5,
    "message": {
      "type": "IdlingMessage",
      "startTime": "2017-08-20T17:27:50Z",
      "duration": 566
    },
    "header": {
      "timestamp": "2017-08-20T13:37:18-04:00",
      "tripType": "IgnitionOff",
      "tripNumber": 21,
      "messageType": 6,
      "messageLength": 7,
      "latitude": 42.299320220947266,
      "longitude": -85.19763946533203,
      "fixQuality": "FixOk",
      "vehicleProtocolId": "ISO15765_29_BIT_CAN",
      "odo": 190
    },
    "isError": false
  }
}
```
