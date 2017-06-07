# Trip start

## Attributes

- body (object)
  - footer: `94` (number) - Contains a checksum for the message contents.
  - message: (object) - Contains the contents of the event.
    - type: `TripStartEvent` (string) - Indicates a type for this event.
    - tripNumber: `46`(number) - A sequential number that increases after each trip. Resets after 65,536 trips.
    - milStatus: `0` (number) - Always zero. 
    - vin: `1C16G05GV2B104942` (string) - Vehicle Identification Number provided by the vehicle.
    - imei: `354235053108415` (string) - International Mobile Equipment Identity number, unique to every Danlaw Datalogger.
  - header (object) - UDP-specifc object containing meta-data about the event.
    - timestamp: `2017-02-13T15:04:49-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - tripType: `Trip` (enum[string]) - Indicates a contextual type for this event.
      - Members
        - `IgnitionOff`
        - `Trip`
        - `Idling`
        - `Unknown`
    - tripNumber: `46` (number) - A sequential number that increases after each trip. Resets after 65,536 trips.
    - messageType: `8` (number) - 
    - messageLength: `40` (number) - Indicates the total bytes of the message, including the checksum.
    - latitude: `42.28004455566406` (number)
    - longitude: `-83.74847412109401` (number)
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
    - odo: `97` (number) - Vehicle odometer or device-calculated odometer.

## Example

```json
{
  "header": {...},
  "body": {
      "footer": 4,
      "message": {
      "type": "TripStartEvent",
      "tripNumber": 46,
      "milStatus": 0,
      "vin": "1C16G05GV2B104942",
      "imei": "354235053108415"
    },
    "header": {
      "timestamp": "2017-02-13T15:04:49-05:00",
      "tripType": "Trip",
      "tripNumber": 46,
      "messageType": 8,
      "messageLength": 40,
      "latitude": 42.28004455566406,
      "longitude": -83.74847412109401,
      "fixQuality": "FixOk",
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "odo": 97
    }
  }
}
```
