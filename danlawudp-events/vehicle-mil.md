# Vehicle MIL

## Attributes

- body (object)
  - footer: `229` (number) - Contains a checksum for the message contents.
  - message: (object) - Contains the contents of the event.
    - type: `VehicleMILInfo` (string) - Indicates a type for this event.
    - milStatus: `true` - Whether the Malfunction Indicator Lamp is on or not.
    - milDistance: `1000` - Distance travelled with MIL on in kilometers.
    - milTime: `1000` - Time travelled with MIL on in minutes.
    - dtcCount: `11` - Number of current DTCs.
    - clrTime: `0` - Time since a DTC was cleared in minutes.
    - clrDistance: `0` - Distance travelled since a DTC was cleared in kilometers.
    - deviceTripTime: `6633` - Accumulated trip time since the first time device stored this MIL info in seconds.
    - deviceTripDistance: `8`- Accumulated distance travelled during this trip since the first time device storied this MIL info in kilometers.
  - header (object) - UDP-specifc object containing meta-data about the event.
    - timestamp: `2017-09-21T17:31:42-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - tripType: `Trip` (enum[string]) - Indicates a contextual type for this event.
      - Members
        - `IgnitionOff`
        - `Trip`
        - `Idling`
        - `Unknown`
    - tripNumber: `333`(number) - A sequential number that increases after each trip. Resets after 65,536 trips.
    - messageType: `50` (number) -
    - messageLength: `19` (number) - Indicates the total bytes of the message, including the checksum.
    - latitude: `42.2782938559` (number)
    - longitude: `-83.7429835754` (number)
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
    - odo: `8323` (number) - Vehicle odometer or device-calculated odometer.

## Example

```json
{
  "header": {...},
  "body": {
    "footer": 112,
    "message": {
      "type": "VehicleMILInfo",
      "milStatus": true,
      "milDistance": 1000,
      "milTime": 1000,
      "dtcCount": 11,
      "clrTime": 0,
      "clrDistance": 0,
      "deviceTripTime": 6633,
      "deviceTripDistance": 8,
    },
    "header": {
      "timestamp": "2017-09-21T17:31:42-05:00",
      "tripType": "Trip",
      "tripNumber": 333,
      "messageType": 50,
      "messageLength": 19,
      "latitude": 42.2782938559,
      "longitude": -83.7429835754,
      "fixQuality": "FixOk",
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "odo": 8323
    },
    "isError": false
  }
}
```
