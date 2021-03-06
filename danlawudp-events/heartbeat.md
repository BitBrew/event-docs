# Heartbeat Event
If no other activity has taken place, the device sends a GPS event 24 hours after its last connection to provide its location.

## Attributes

- body (object)
  - footer: `186` (number) - Contains a checksum for the message contents.
  - message: (object) - Contains the contents of the event.
      - type: `GPSMessage` (string) - Indicates a type for this event.
      - messageTriggerReason: `KeyOff` (enum[string])
      - cog: `0` (number) - Indicates change in course over ground in degrees relative to true north.
      - obdSpeed: `0` (number) - Vehicle speed in KPH.
      - height: `0` (number) - Height above sea level in meters.
      - tripDistance: `0` (number) - Distance travelled thus far in the trip in kilometers.
      - vehicleODOStatus: `VehicleODONotSupported` (enum[string]) - Indicates whether or not the device can read from the vehicle's odometer.
        - Members
          - `VehicleODONotSupported` -  Vehicle odometer readings are not supported.
          - `VehicleODOSupported` - Vehicle odometer readings are supported.
      - obdAverageSpeed: `0` (number) - Average vehicle speed thus far in the trip in KPH.
      - hdop: `0` (number) - See [Horizontal Dilution of Precision](../horizontal-dillution-of-precision.md) for more information.
      - sv: `0` (number) - How many satellites the device is tracking for GPS.
      - obdMaxSpeed: `0` (number) - Maximum recorded speed thus far in the trip in KPH.
      - tripIdlingTime: `0` (number) - Amount of time spent idling thus far in the trip in seconds.
      - sog: `0` (number) - Speed over ground.
      - fixQuality: `GPSNoFix` (enum[string]) - Determines the validity and accuracy of the GPS data.
        - Members
          - `GPSNoFix` - Latitude and longitude are invalid.
          - `GPS2DFix` - Latitude and longitude are valid.
          - `GPS3DFix` - Latitude and longitude are valid.
          - `Unknown`
  - header (object) - UDP-specifc object containing meta-data about the event.
    - timestamp: `2016-02-05T10:36:31-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - tripType: `Trip` (enum[string]) - Indicates a contextual type for this event.
      - Members
        - `IgnitionOff`
        - `Trip`
        - `Idling`
        - `Unknown`
    - tripNumber: `0`- A sequential number that increases after each trip. Resets after 65,536 trips.
    - messageType: `40` (number) - 
    - messageLength: `40` (number) - Indicates the total bytes of the message, including the checksum.
    - latitude: `42.2793934` (number)
    - longitude: `-83.72955975` (number)
    - fixQuality: `FixInvalid` (enum[string]) - The validity and accuracy of the GPS data.
      - Members
        - `FixOk` - 2D or 3D fix. Latitude and longitude are valid.
        - `StoredFix` - Latitude and longitude are readings from (up to) 5 seconds ago, because the device has not been able to get a GPS fix for 5 seconds.
        - `FixInvalid` - Latitude and longitude are invalid.
        - `Unknown` - The platform cannot decode the value.
    - vehicleProtocolId: `NoProtocol` (enum[string]) - The type of protocol the device detected on the vehicle bus.
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
    "footer": 186,
    "message": {
      "type": "GPSMessage",
      "messageTriggerReason": "KeyOff",
      "cog": 0,
      "obdSpeed": 0,
      "height": 0,
      "tripDistance": 0,
      "vehicleODOStatus": "VehicleODONotSupported",
      "obdAverageSpeed": 0,
      "hdop": 0,
      "sv": 0,
      "obdMaxSpeed": 0,
      "tripIdlingTime": 0,
      "sog": 0,
      "fixQuality": "GPSNoFix"
    },
    "header": {
      "timestamp": "2016-10-03T15:37:32-04:00",
      "tripType": "IgnitionOff",
      "tripNumber": 2,
      "messageType": 1,
      "messageLength": 16,
      "latitude": 0,
      "longitude": 0,
      "fixQuality": "FixInvalid",
      "vehicleProtocolId": "NoProtocol",
      "odo": 0
    },
    "isError": false
  }
}
```
