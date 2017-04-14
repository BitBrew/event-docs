# Device Communication

## <a name="device-connected"></a> Device Connected

### Properties

Currently unavailable

### Example

```json
{
  "header": {...},
  "body": {
    "header": {
      "imei": "354235053108415",
      "evtDataAvl": 1,
      "cfgVersion": "BBRTS.05",
      "vin": "JM1BK343551221507",
      "swVersion": "07.46",
      "pctTripData": 1
    },
    "contents": {
      "command1": "NEW",
      "result": 0,
      "reportType": 3,
      "command2": "EVNT"
    }
  }
}
```

## <a name="data-upload-completed"></a> Data Upload Completed

### Properties

Currently unavailable

## Example

```json
{
  "header": {...},
  "body": {
    "procVersion": 1,
    "command1": "GET",
    "result": 1,
    "byteCount": 0,
    "packSerial": 0,
    "command2": "DATA",
    "recordInfo": 0
  }
}
```

## <a name="update-command-confirmed"></a> Update Command Confirmed

## Properties

Currently unavailable

## Example

```json
{
  "header": {...},
  "body": {
    "command1": "SET",
    "result": 1,
    "command2": "UPDT",
    "errorCode": 300
  }
}
```
