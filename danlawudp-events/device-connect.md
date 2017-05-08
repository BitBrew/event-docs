# Device Connect

## Properties
- body: (object)
  - footer: `83` (number) - Contains a checksum for the message contents.
  - message: (object) - Contains the contents of the event.
    - type: `ConnectDisconnectEvent` (string) - Indicates a type for this event.
    - eventType: `Connect` (string) - Further specifies the type of event.
    - eventTime: `2016-12-29T10:52:14-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - firmwareVersion: `07.2E` (string) - The name of the firmware file that the device is running.
    - cfgVersion: `JHGDL13` (string) - The name of the configuration file that the device is running.
    - keyOnOffDisconnect: `KeyOffDisconnect` (enum[string]) 
      - Members
        - `KeyOnDisconnect`
        - `KeyOffDisconnect`
    - odometer: `28` (number) - Vehicle odometer or device-calculated odometer (see `odometerInfo` for differentiator).
    - odometerInfo: `VehicleOdometer` (enum[string]) - Indicates whether the `odometer` value is read from the vehicle or the device.
      - Members
        - `Calculated` - Indicates that the `odometer` value came from the device.
        - `VehicleOdometer` - Indicates that the `odometer` value was read from the vehicle.
  - header (object) - UDP-specifc object containing meta-data about the event.
    - timestamp: `2017-06-01T11:42:14-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - tripType: `Trip`(enum[string]) - Indicates a contextual type for this event.
      - Members
        - `IgnitionOff`
        - `Trip`
        - `Idling`
        - `Unknown`
    - tripNumber: `2`- A sequential number that increases after each trip. Resets after 65,536 trips.
    - messageType: `14` (number) - 
    - messageLength: `32` (number) - Indicates the total bytes of the message, including the checksum.
    - latitude: `42.2891150` (number)
    - longitude: `-83.72973914` (number)
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
    - odo: `0` (number) - Vehicle odometer or device-calculated odometer.


## Example

```json
{
  "header": {...},
  "body": {
      "footer": 83,
      "message": {
        "type": "ConnectDisconnectEvent",
        "eventType": "Connect",
        "eventTime": "2017-06-01T11:42:13-05:00",
        "firmwareVersion": "07.2E",
        "cfgVersion": "JHGDL13",
        "keyOnOffDisconnect": "KeyOffDisconnect",
        "odometer": 28,
        "odometerInfo": "VehicleOdometer"
      },
      "header": {
        "timestamp": "2017-06-01T11:42:14-05:00",

        "tripType": "Trip",
        "tripNumber": 2,
        "messageType": 14,
        "messageLength": 32,
        "latitude": 42.2891150,
        "longitude": -83.72973914,
        "fixQuality": "FixOk",
        "vehicleProtocolId": "ISO15765_11_BIT_CAN",
        "odo": 0
      },
    "isError": false
  }
}
```
