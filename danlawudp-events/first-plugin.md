# First Plugin

## Properties

- body (object)
  - footer: `152` (number) - Contains a checksum for the message contents.
  - message: (object) - Contains the contents of the event.
    - firmwareVersion: `07.2E` (string) -
    - odometerValue: `0` (number) - Vehicle odometer or device-calculated odometer (see `additionalInfo` for differentiator).
    - configVersion: `072E.1` (string) - 
    - vin: `1F1G05GV2B1049415` - Vehicle Identification Number provided by the vehicle. Empty string when VIN is unavailable.
    - additionalInfo: `VehicleOdometer` (enum[string]) - Indicates whether the `odometerValue` is read from the vehicle or the device.
    - type: `FirstPluginEvent` (string) - Indicates a type for this event.
  - header (object) - UDP-specifc object containing meta-data about the event.
    - timestamp: `2016-02-05T10:36:31-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - latitude: `42.2793934` (number)
    - tripType: `Trip`(enum[string]) - Indicates a contextual type for this event.
      - Members
        - `IgnitionOff`
        - `Trip`
        - `Idling`
        - `Unknown`
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
    - longitude: `-83.72955975` (number)
    - messageType: `40` (number) - 
    - odo: `22` (number) - Vehicle odometer or device-calculated odometer.
    - tripNumber: `23`- A sequential number that increases after each trip. Resets after 65,536 trips.
    - fixQuality: `FixInvalid` (enum[string]) - The validity and accuracy of the GPS data.
      - Members
        - `FixOk` - 2D or 3D fix. Latitude and longitude are valid.
        - `StoredFix` - Latitude and longitude are readings from (up to) 5 seconds ago, because the device has not been able to get a GPS fix for 5 seconds.
        - `FixInvalid` - Latitude and longitude are invalid.
        - `Unknown` - The platform cannot decode the value.
    - messageLength: `40`(number) - Indicates the total bytes of the message, including the checksum.

## Example

```json
{
  "header": {...},
  "body": {
    "footer": 152,
    "message": {
      "firmwareVersion": "07.2E",
      "odometerValue": 0,
      "configVersion": "072E.1",
      "vin": "1F1G05GV2B1049415",
      "additionalInfo": "VehicleOdometer",
      "type": "FirstPluginEvent"
    },
    "header": {
      "timestamp": "2016-10-03T15:37:32-04:00",
      "latitude": 0,
      "tripType": "Trip",
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "longitude": 0,
      "messageType": 40,
      "odo": 0,
      "tripNumber": 0,
      "fixQuality": "FixInvalid",
      "messageLength": 40
    },
    "isError": false
  }
}
```
