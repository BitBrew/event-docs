# IO Extender
This event provides input data and digital output status data for analog channels if an IO extender module is attached to the device.

## Attributes

- body (object)
  - footer: `195` (number) - Contains a checksum for the message contents.
  - message: (object) - Contains the contents of the event.
    - type: `IoExtenderAnalogDigitalChannelEvent` (string) - Indicates a type for this event.
    - analogChannel0: `0.008813186548650265` (number) - The analog channel input in volts.
    - analogChannel1: `0.0` (number) - The analog channel input in volts.
    - analogChannel2: `0.0` (number) - The analog channel intput in volts.
    - analogChannel3: `0.0` (number) - The analog channel intput in volts.
    - analogChannel4: `0.0` (number) - The analog channel intput in volts.
    - analogChannel5: `0.0` (number) - The analog channel intput in volts.
    - isDigitalOutputHigh: `false` (boolean) - Indicates whether the digital output status is high or low.
  - header (object) - UDP-specifc object containing meta-data about the event.
    - timestamp: `2017-03-16T14:29:11-04:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - tripType: `Trip`(enum[string]) - Indicates a contextual type for this event.
      - Members
        - `IgnitionOff`
        - `Trip`
        - `Idling`
        - `Unknown`
    - tripNumber: `35`- A sequential number that increases after each trip. Resets after 65,536 trips.
    - messageType: `54` (number) - 
    - messageLength: `15` (number) - Indicates the total bytes of the message, including the checksum.
    - latitude: `42.47819519042969` (number)
    - longitude: `-83.45089721679688` (number)
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
    - odo: `537` (number) - Vehicle odometer or device-calculated odometer.

## Example
```
{
  "header": {...},
  "body": {
    "footer": 0,
    "message": {
      "type": "IoExtenderAnalogDigitalChannelEvent",
      "analogChannel0": 0.008813186548650265,
      "analogChannel1": 0.0,
      "analogChannel2": 0.0,
      "analogChannel3": 0.0,
      "analogChannel4": 0.0,
      "analogChannel5": 0.0,
      "isDigitalOutputHigh": false
    },
    "header": {
      "timestamp": "2017-03-16T14:29:11-04:00",
      "tripType": "Trip",
      "tripNumber": 35,
      "messageType": 54,
      "messageLength": 15,
      "latitude": 42.47819519042969,
      "longitude": -83.45089721679688,
      "fixQuality": "FixOk",
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "odo": 537
    }
  }
}
```
