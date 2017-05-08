# Vehicle Movement

## Attributes

- body (object)
  - footer: `30` (number) - Contains a checksum for the message contents.
  - message: (object) - Contains the contents of the event.
    - type: `VehicleMovementEvent` (string) - Indicates a type for this event.
    - movementEventType: `Stopped` (enum[string]) - Whether the vehicle is still in motion or has stopped.
      - Members
        - `Moving`
        - `Stopped`
        - `Unknown`
  - header (object) - UDP-specifc object containing meta-data about the event.
    - timestamp: `2017-02-05T12:56:03-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - tripType: `Trip` (enum[string]) - Indicates a contextual type for this event.
      - Members
        - `IgnitionOff`
        - `Trip`
        - `Idling`
        - `Unknown`
    - tripNumber: `26`(number) - A sequential number that increases after each trip. Resets after 65,536 trips.
    - messageType: `16` (number) -
    - messageLength: `2` (number) - Indicates the total bytes of the message, including the checksum.
    - latitude: `42.47832489013672` (number)
    - longitude: `-83.45087432861328` (number)
    - fixQuality: `FixOk` (enum[string]) - The validity and accuracy of the GPS data.
      - Members
        - `FixOk` - 2D or 3D fix. Latitude and longitude are valid.
        - `StoredFix` - Latitude and longitude are readings from (up to) 5 seconds ago, because the device has not been able to get a GPS fix for 5 seconds.
        - `FixInvalid` - Latitude and longitude are invalid.
        - `Unknown` - The platform cannot decode the value.
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
    - odo: `784` (number) - Vehicle odometer or device-calculated odometer.

## Example

```json
{
  "header": {...},
  "body": {
    "footer": 30,
    "message": {
      "type": "VehicleMovementEvent",
      "movementEventType": "Stopped"
    },
    "header": {
      "timestamp": "2017-02-05T12:56:03-05:00",
      "tripType": "Trip",
      "tripNumber": 26,
      "messageType": 16,
      "messageLength": 2,
      "latitude": 42.47832489013672,
      "longitude": -83.45087432861328,
      "fixQuality": "FixOk", 
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "odo": 784
    },
    "isError": false
  }
}
```
