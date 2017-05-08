# Vehicle DTCs - Current

This event is generated whenver a MIL status or DTC count changes and a current DTC exists in the vehicle. The device can be configured to check for DTCs once per trip or at periodic intervals.

## Attributes

- body (object)
  - footer: `67` (number) - Contains a checksum for the message contents.
  - message: (object) - Contains the contents of the event.
    - type: `VehicleCurrentDTCInfo` (string) - Indicates a type for this event.
    - milStatus: `true` (boolean) - Whether the Malfunction Indicator Lamp is on or not.
    - dtcSpnOrPidRecords: (array) - A list of current DTC codes.
        - `P3412`
        - `C2745`
        - `B0888`
        - `P2222`
  - header (object) - UDP-specifc object containing meta-data about the event.
    - timestamp: `2017-11-16T17:31:28-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - tripType: `Trip` (enum[string]) - Indicates a contextual type for this event.
      - Members
        - `IgnitionOff`
        - `Trip`
        - `Idling`
        - `Unknown`
    - tripNumber: `33`(number) - A sequential number that increases after each trip. Resets after 65,536 trips.
    - messageType: `18` (number) -
    - messageLength: `15` (number) - Indicates the total bytes of the message, including the checksum.
    - latitude: `0` (number)
    - longitude: `0` (number)
    - fixQuality: `FixInvalid` (enum[string]) - The validity and accuracy of the GPS data.
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
    - odo: `400` (number) - Vehicle odometer or device-calculated odometer.

## Example

```json
{
  "header": {...},
  "body": {
    "footer": 67,
    "message": {
      "type": "VehicleCurrentDTCInfo",
      "milStatus": true,
      "dtcSpnOrPidRecords": [
        "P3412",
        "C2745",
        "B0888",
        "P2222"
      ]
    },
    "header": {
      "timestamp": "2017-11-16T17:31:28-05:00",
      "tripType": "Trip",
      "tripNumber": 33,
      "messageType": 18,
      "messageLength": 15,
      "latitude": 0,
      "longitude": 0,
      "fixQuality": "FixInvalid",
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "odo": 400
    },
    "isError": false
  }
}
```
