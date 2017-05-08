# Device Disconnect

## Properties

- body: (object)
  - footer: `128` (number) - Contains a checksum for the message contents.
  - message: (object) - Contains the contents of the event.
    - type: `ConnectDisconnectEvent` (string) - Indicates a type for this event.
    - eventType: `Disconnect` (string) - Further specifies the type of event.
    - eventTime: `22017-08-29T17:46:58-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - firmwareVersion: `07.2E` (string) - The name of the firmware file that the device is running.
    - cfgVersion: `JHGDL13` (string) - The name of the configuration file that the device is running.
    - keyOnOffDisconnect: `KeyOffDisconnect` (enum[string]) 
      - Members
        - `KeyOnDisconnect`
        - `KeyOffDisconnect`
    - odometer: `135857` (number) - Vehicle odometer or device-calculated odometer (see `odometerInfo` for differentiator).
    - odometerInfo: `VehicleOdometer` (enum[string]) - Indicates whether the `odometer` value is read from the vehicle or the device.
      - Members
        - `Calculated` - Indicates that the `odometer` value came from the device.
        - `VehicleOdometer` - Indicates that the `odometer` value was read from the vehicle.
  - header (object) - UDP-specifc object containing meta-data about the event.
    - timestamp: `2017-08-29T17:46:58-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - latitude: `42.478084564208984` (number)
    - tripType: `Trip`(enum[string]) - Indicates a contextual type for this event.
      - Members
        - `IgnitionOff`
        - `Trip`
        - `Idling`
        - `Unknown`
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
    - longitude: `-83.45092010498047` (number)
    - messageType: `14` (number) - 
    - odo: `5623` (number) - Vehicle odometer or device-calculated odometer.
    - tripNumber: `890`- A sequential number that increases after each trip. Resets after 65,536 trips.
    - fixQuality: `FixOk` (enum[string]) - The validity and accuracy of the GPS data.
      - Members
        - `FixOk` - 2D or 3D fix. Latitude and longitude are valid.
        - `StoredFix` - Latitude and longitude are readings from (up to) 5 seconds ago, because the device has not been able to get a GPS fix for 5 seconds.
        - `FixInvalid` - Latitude and longitude are invalid.
        - `Unknown` - The platform cannot decode the value.
    - messageLength: `32` (number) - Indicates the total bytes of the message, including the checksum.

## Example

```json
{
  "header": {...},
  "body": {
    "footer": 128,
    "message": {
      "type": "ConnectDisconnectEvent",
      "eventType": "Disconnect",
      "eventTime": "2017-08-29T17:46:58-05:00",
      "firmwareVersion": "07.2E",
      "cfgVersion": "JHGDL13",
      "keyOnOffDisconnect": "KeyOffDisconnect",
      "odometer": 135857,
      "odometerInfo": "VehicleOdometer"
    },
    "header": {
      "timestamp": "2017-08-29T17:46:58-05:00",
      "latitude": 42.478084564208984,
      "tripType": "Trip",
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "longitude": -83.45092010498047,
      "messageType": 14,
      "odo": 0,
      "tripNumber": 890,
      "fixQuality": "FixOk",
      "messageLength": 32
    },
    "isError": false
  }
}
```
