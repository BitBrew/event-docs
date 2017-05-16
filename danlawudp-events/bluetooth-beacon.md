# Bluetooth Beacon
This event sends information about specific drivers detected in the vehicle via Bluetooth® beacon cards. Up to four beacons can be detected, and information about the beacons—including their unique MAC addresses and their relative signal strengths—are contained in the `beaconInfo` object.

## Properties
- body: (object)
  - footer: `206` (number) - Contains a checksum for the message contents.
  - message: (object) - Contains the contents of the event.
    - type: `BluetoothBeaconMessage` (string) - Indicates a type for this event.
    - beaconInfo: (array[object])
        - type: `BeaconInfo` (string) -  Specifies the category of fields in this object.
        - bluetoothAddress: `417706011` (number) - Unique MAC address used to identify the Bluetooth® beacon.
        - visibilityScore: `232` (number) - Relative indicator of signal strength. A lower score is a stronger signal. 
  - header (object) - UDP-specifc object containing meta-data about the event.
    - timestamp: `2017-02-05T12:55:34-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - tripType: `Trip` (enum[string]) - Indicates a contextual type for this event.
      - Members
        - `IgnitionOff`
        - `Trip`
        - `Idling`
        - `Unknown`
    - tripNumber: `6` (number) - A sequential number that increases after each trip. Resets after 65,536 trips.
    - messageType: `30` (number) - 
    - messageLength: `24` (number) - Indicates the total bytes of the message, including the checksum.
    - latitude: `42.47832489013763` (number)
    - longitude: `-83.45087432866512` (number)
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
    - odo: `45` (number) - Vehicle odometer or device-calculated odometer.

## Example

```json
{
  "header": {...},
  "body": {
    "footer": 206,
    "message": {
      "type": "BluetoothBeaconMessage",
      "beaconInfo": [{
        "type": "BeaconInfo",
        "bluetoothAddress": 4177060611,
        "visibilityScore": 232,
      }]
    },
    "header": {
      "timestamp": "2017-02-05T12:55:34-05:00",
      "tripType": "Trip",  
      "tripNumber": 6,  
      "messageType": 30,  
      "messageLength": 24,  
      "latitude": 42.47832489013763,
      "longitude": -83.45087432866512,  
      "fixQuality": "FixOk",
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "odo": 45
    },
    "isError": false
  }
}
```
