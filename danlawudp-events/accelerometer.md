# Accelerometer

Accelerometers measure acceleration in meters per second squared
(m/s<sup>2</sup>) or G-forces (g). A single G-force unit is equal to 9.8
m/s<sup>2</sup>. A g is equal to 1000mG.

Acceleromeeter events are generated using 24Hz accelerometer sampling with
sensitivity up to 2g. The threshold for triggering the event and the minimum
number of samples needed to verify the event are configurable. The number of
milliseconds the threshold must be maintained is static (1000 milliseconds).

The `ImpactEvent` is generated using 100Hz accelerometer sampling and can provide
readings up to 16g. The threshold for triggering the impact event, the number of
milliseconds the threshold must be maintained, and the minimum number of samples
needed to verify the impact event are all configurable.

## Attributes
- body: (object)
  - footer: `227` - Contains a checksum for the message contents.
  - message: (object) - Contains the contents of the event.
    - type: `AccelerometerEvent` (string) - Indicates a type for this event.
    - eventType: `ImpactEvent` (enum[string]) - The type of accelerometer event.
      - Members
        - `ImpactEvent` - An impact event was generated because the impact criteria were met.
        - `HardAccl` - A hard acceleration event was generated because the configured event criteria were met.
        - `HardBraking`- A hard braking event was generated because the configured event criteria were met.
        - `HardTurn` - A hard turn event was generated because the configured event criteria were met.
        - `Unknown` - The platform is unable to determine the accelerometer event type.
    - triggerValue: `518` (number) - The configured threshold for this event type in mG.
    - maxValue: `518` (number) - The maximum value reached for this event in mG.
  - header (object) - UDP-specifc object containing meta-data about the event.
    - timestamp: `2017-02-05T10:36:31-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - tripType: `Trip`(enum[string]) - Indicates a contextual type for this event.
      - Members
        - `IgnitionOff`
        - `Trip`
        - `Idling`
        - `Unknown`
    - tripNumber: `23`- A sequential number that increases after each trip. Resets after 65,536 trips.
    - messageType: `10` (number) - 
    - messageLength: `6` (number) - Indicates the total bytes of the message, including the checksum.
    - latitude: `42.27866889` (number)
    - longitude: `-83.74376147` (number)
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
    - odo: `22` (number) - Vehicle odometer or device-calculated odometer.

## Example

```json
{
  "header": {...},
  "body": {
    "footer": 227,
    "message": {
      "type": "AccelerometerEvent",
      "eventType": "ImpactEvent",
      "triggerValue": 518,
      "maxValue": 518
    },
    "header": {
      "timestamp": "2017-02-05T10:36:31-05:00",
      "tripType": "Trip",
      "tripNumber": 23,
      "messageType": 10,
      "messageLength": 6,
      "latitude": 42.27866889,
      "longitude": -83.74376147,
      "fixQuality": "FixOk",
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "odo": 22
    },
    "isError": false
  }
}
```
