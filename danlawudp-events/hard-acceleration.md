# Hard Acceleration
An acceleration event is generated if the vehicle's acceleration and speed are greater than or equal to the device's configured thresholds. This event can be multiple seconds long.

## Attributes
- body (object)
  - footer: `209` (number) - Contains a checksum for the message contents.
  - message: (object ) - Contains the contents of the event.
    - type: `HardAccelerationMessage` (string) - Indicates a type for this event.
    - initialSpeed: `6` (number) - Vehicle speed at the beginning of the acceleration event in KPH.
    - finalSpeed: `22` (number) - Vehicle speed at the end of the acceleration event in KPH.
    - maxAcceleration: `11` (number) - Maximum acceleration reached during the event in KPH/s.
  - header (object) - UDP-specifc object containing meta-data about the event.
    - timestamp: `2017-11-18T16:14:34-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - tripType: `Trip`(enum[string]) - Indicates a contextual type for this event.
      - Members
        - `IgnitionOff`
        - `Trip`
        - `Idling`
        - `Unknown`
    - tripNumber: `304`- A sequential number that increases after each trip. Resets after 65,536 trips.
    - messageType: `5` (number) - 
    - messageLength: `4` (number) - Indicates the total bytes of the message, including the checksum.
    - latitude: `42.478797912597656` (number)
    - longitude: `-83.45558166503906` (number)
    - fixQuality: `FixOk` (enum[string]) - The validity and accuracy of the GPS data.
      - Members
        - `FixOk` - 2D or 3D fix. Latitude and longitude are valid.
        - `StoredFix` - Latitude and longitude are readings from (up to) 5 seconds ago, because the device has not been able to get a GPS fix for 5 seconds.
        - `FixInvalid` - Latitude and longitude are invalid.
        - `Unknown` - The platform cannot decode the value.
    - vehicleProtocolId: `ISO9141`(enum[string]) - The type of protocol the device detected on the vehicle bus.
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
    - odo: `375` (number) - Vehicle odometer or device-calculated odometer.

## Example

```json
{
  "header": {...},
  "body": {
    "footer": 209,
    "message": {
      "type": "HardAccelerationMessage",
      "initialSpeed": 6,
      "finalSpeed": 22,
      "maxAcceleration": 11
    },
    "header": {
      "timeStamp": "2017-11-18T16:14:34-05:00",
      "tripType": "Trip",
      "tripNumber": 304,
      "messageType": 5,
      "messageLength": 4,
      "latitude": 42.478797912597656,
      "longitude": -83.45558166503906,
      "fixQuality": "FixOk",
      "vehicleProtocolId": "ISO9141",
      "odo": 375
    },
    "isError": false
  }
}
```
