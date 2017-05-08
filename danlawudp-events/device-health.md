# Device Health

## Attributes
- body (object)
  - footer: `102` (number) - Contains a checksum for the message contents.
  - message: (object) - Contains the contents of the event.
    - type: `DeviceHealthEvent` (strng) - Indicates a type for this event.
    - faultGroup: `Information` (enum[string]) - Assigns a category for the type of fault the device is encountering.
      - `Critical`
      - `Major`
      - `Information`
      - `Unknown`
    - faultInformation: (object) - Contains information about the fault.
        - primaryAndSecondaryErrorCount: `0`
        - type: `ConfigFailure`
        - temporaryErrorCount": `0`
    - faultId: `29` - Corresponds to the `type` of fault listed in the `faultInformation` object.
    - faultRecoveryAction: `SafeMode` (enum[string) - Action that the device took to correct the fault.
      - Members
        - `ClearFault`
        - `KillDevice`
        - `SuspendDevice`
        - `ResetDevice`
        - `NoAction`
        - `SafeMode`
        - `Unknown`
  - header (object) - UDP-specifc object containing meta-data about the event.
    - timestamp: `2017-11-18T16:14:34-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
    - tripType: `IgnitionOff`(enum[string]) - Indicates a contextual type for this event.
      - Members
        - `IgnitionOff`
        - `Trip`
        - `Idling`
        - `Unknown`
    - tripNumber: `0`- A sequential number that increases after each trip. Resets after 65,536 trips.
    - messageType: `15` (number) - 
    - messageLength: `6` (number) - Indicates the total bytes of the message, including the checksum.
    - latitude: `42.2793934` (number)
    - longitude: `-83.72955975` (number)
    - fixQuality: `FixInvalid` (enum[string]) - The validity and accuracy of the GPS data.
      - Members
        - `FixOk` - 2D or 3D fix. Latitude and longitude are valid.
        - `StoredFix` - Latitude and longitude are readings from (up to) 5 seconds ago, because the device has not been able to get a GPS fix for 5 seconds.
        - `FixInvalid` - Latitude and longitude are invalid.
        - `Unknown` - The platform cannot decode the value.
    - vehicleProtocolId: `NoProtocol`(enum[string]) - The type of protocol the device detected on the vehicle bus.
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
    - odo: `100` (number) - Vehicle odometer or device-calculated odometer.
    
## Example

```json
{
  "header": {...},
  "body": {
    "footer": 102,
    "message": {
      "type": "DeviceHealthEvent",
      "faultGroup": "Information",
      "faultInformation": {
        "primaryAndSecondaryErrorCount": 0,
        "type": "ConfigFailure",
        "temporaryErrorCount": 0
      },
      "faultId": 29,
      "faultRecoveryAction": "SafeMode",
    }
    "header": {
      "timestamp": "2017-11-18T16:14:34-05:00",
      "tripType": "IgnitionOff",
      "tripNumber": 35,
      "messageType": 15,
      "messageLength": 6,
      "latitude": 0,
      "longitude": 0,
      "fixQuality": "FixInvalid",
      "vehicleProtocolId": "NoProtocol",
      "odo": 100
    },
    "isError": false
  }
}
```
