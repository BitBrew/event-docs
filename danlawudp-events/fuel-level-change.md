# Fuel Level Change
This event message is generated whenever there is a significant change in Fuel Level between the Trip End and Trip Start.

- body (object)
  - footer: `227` (number) - Contains a checksum for the message contents.
  - message: (object) - Contains the contents of the event.
    - type: `FuelLevelChangeEvent` (string) - Indicates a type for this event.
    - fuelEventType: `FuelLevelDecrease` (enum[string]) - Indicates whether fuel has increased or decreased
      - Members
        - `FuelLevelIncrease`
        - `FuelLevelDecrease`
    - previousFuelLevel: `54` (number) - Percentage
    - currentFuelLevel: `14` (number) - Percentage
    - cumulativeFuelConsumed: `5.394000053405762` (number) - Resolution of 0.001 gallons
  - header (object) - UDP-specifc object containing meta-data about the event.
    - timestamp: `2017-03-31T20:12:18-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - tripType: `IgnitionOff` (enum[string]) - Indicates a contextual type for this event.
      - Members
        - `IgnitionOff`
        - `Trip`
        - `Idling`
        - `Unknown`
    - tripNumber: `3`(number) - A sequential number that increases after each trip. Resets after 65,536 trips.
    - messageType: `17` (number) -
    - messageLength: `37` (number) - Indicates the total bytes of the message, including the checksum.
    - latitude: `42.279937744140625` (number)
    - longitude: `-83.74799346923828` (number)
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
    - odo: `88` (number) - Vehicle odometer or device-calculated odometer.

## Example

```json
{
  "header": {...},
  "body": {
    "footer": 227,
    "message": {
      "type": "FuelLevelChangeEvent",
      "fuelEventType": "FuelLevelDecrease",
      "previousFuelLevel": 54,
      "currentFuelLevel": 14,
      "cumulativeFuelConsumed": 5.394000053405762
    },
    "header": {
      "timeStamp": "2017-03-31T20:12:18-05:00",
      "tripType": "IgnitionOff",
      "tripNumber": 3,
      "messageType": 17,
      "messageLength": 37,
      "latitude": 42.279937744140625,
      "longitude": -83.74799346923828,
      "fixQuality": "FixOk",
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "odo": 88
    },
    "isError": false
  }
}
```
