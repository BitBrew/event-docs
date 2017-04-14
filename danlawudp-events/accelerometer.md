# Accelerometer

Accelerometers measure acceleration in meters per second squared
(m/s<sup>2</sup>) or G-forces (g). A single G-force unit is equal to 9.8
m/s<sup>2</sup>. A g is equal to 1000mG.

The impact event is generated using 100Hz accelerometer sampling and can provide
readings up to 16g. The threshold for triggering the impact event, the number of
milliseconds the threshold must be maintained, and the minimum number of samples
needed to verify the impact event are all configurable.

All other events are generated using 24Hz accelerometer sampling with
sensitivity up to 2g. The threshold for triggering the event and the minimum
number of samples needed to verify the event are configurable. The number of
milliseconds the threshold must be maintained is static (1000 milliseconds).

## Attributes

- maxValue: `518` (number) - The maximum value reached for this event in mG.
- triggerValue: `518` (number) - The configured threshold for this event type in mG.
- eventType: `ImpactEvent` (enum[string]) - The type of accelerometer event.
  - Members
    - `ImpactEvent` - An impact event was generated because the impact criteria were met.
    - `HardAccl` - A hard acceleration event was generated because the event criteria were met.
    - `HardBraking`- A hard braking event was generated because the event criteria were met.
    - `HardTurn` - A hard turn event was generated because the event criteria were met.
    - `Unknown` - Only generated if the platform is unable to determine the accelerometer event type.
- type: `AccelerometerEvent` (string)

## Example

```json
{
  "header": {...},
  "body": {
    "footer": 227,
    "message": {
      "maxValue": 518,
      "triggerValue": 518,
      "eventType": "ImpactEvent",
      "type": "AccelerometerEvent"
    },
    "header": {
      "timestamp": "2016-02-05T10:36:31-05:00",
      "latitude": 0.0,
      "tripType": "Trip",
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "longitude": 0.0,
      "messageType": 10,
      "odo": 22,
      "tripNumber": 23,
      "fixQuality": "FixInvalid",
      "messageLength": 6
    },
    "isError": false
  }
}
```
