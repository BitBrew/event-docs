# Vehicle DTCs - Pending


## Attributes

- body (object)
  - footer: `67` (number) - Contains a checksum for the message contents.
  - message: (object) - Contains the contents of the event.
    - type: `VehiclePendingDTCInfo` (string) - Indicates a type for this event.
    - dtcSpnOrPidRecords: (array) - A list of pending DTC codes.
        - `P3412`
  - header (object) - UDP-specifc object containing meta-data about the event.
    - timestamp: `2017-05-29T14:47:58-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - tripType: `Trip` (enum[string]) - Indicates a contextual type for this event.
      - Members
        - `IgnitionOff`
        - `Trip`
        - `Idling`
        - `Unknown`
    - tripNumber: `38`(number) - A sequential number that increases after each trip. Resets after 65,536 trips.
    - messageType: `51` (number) -
    - messageLength: `10` (number) - Indicates the total bytes of the message, including the checksum.
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
    - odo: `101928` (number) - Vehicle odometer or device-calculated odometer.

## Example

```json
{
  "header": {...},
  "body": {
    "footer": 229,
    "message": {
      "type": "VehiclePendingDTCInfo",
      "dtcRecords": [
        "P3412"
      ]
    },
    "header": {
      "timestamp": "2017-05-29T14:47:58-05:00",
      "tripType": "Trip", 
      "tripNumber": 38,
      "messageType": 51,  
      "messageLength": 10, 
      "latitude": 0,
      "longitude": 0,
      "fixQuality": "FixInvalid",
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "odo": 101928
    },
    "isError": false
  }
}
```
