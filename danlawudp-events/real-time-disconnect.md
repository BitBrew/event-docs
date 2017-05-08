# Real Time Disconnect

## Attributes

- body (object)
  - footer: `212` (number) - Contains a checksum for the message contents.
  - message: (object) - Contains the contents of the event.
    - type: `RealTimeDisconnectEvent` (string) - Indicates a type for this event.
    - isKeyOn: `false` (boolean) - Indicates whether the vehicle was on at the time the device was disconnected.
    - vin: `JM1BK343551221507` - Vehicle Identification Number provided by the vehicle.
    - vehicleLastKnownLoc: `0` - Distance driven from the last known location in kilometers.
    - vehicleOdoAvailable: `false` (boolean) - Indicates whether the odometer value is read from the vehicle or the device.
    - vehicleOdometer: `0` - Vehicle odometer value.
    - calculatedOdometer": `1667` - Device odometer value.
  - header (object) - UDP-specifc object containing meta-data about the event.
    - timestamp: `2017-08-22T16:08:10-04:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - tripType: `IgnitionOff`(enum[string]) - Indicates a contextual type for this event.
      - Members
        - `IgnitionOff`
        - `Trip`
        - `Idling`
        - `Unknown`
    - tripNumber: `92`- A sequential number that increases after each trip. Resets after 65,536 trips.
    - messageType: `53` (number) - 
    - messageLength: `30` (number) - Indicates the total bytes of the message, including the checksum.
    - latitude: `42.278709411621094` (number)
    - longitude: `-83.74756622314453` (number)
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
    - odo: `1667` (number) - Vehicle odometer or device-calculated odometer.

## Example

```json
{
  "header": {...},
  "body": {
    "footer": 212,
    "message": {
      "type": "RealTimeDisconnectEvent",
      "isKeyOn": false,
      "vin": "JM1BK343551221507",
      "vehicleLastKnownLoc": 0,
      "vehicleOdoAvailable": false
      "vehicleOdometer": 0,
      "calculatedOdometer": 1667,
    },
    "header": {
      "timestamp": "2017-08-22T16:08:10-04:00",
      "tripType": "IgnitionOff",
      "tripNumber": 92,
      "messageType": 53,
      "messageLength": 30,
      "latitude": 42.278709411621094,
      "longitude": -83.74756622314453,
      "fixQuality": "FixOk",
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "odo": 1667
    },
    "isError": false
  }
}
```
