# Trip End

## <a name="trip-end-relative-time"></a> Trip End Relative Time

### Attributes

- type: 'TripEndRecordRelativeTime` - (string) - Indicates a type for this event.
- timestamp: `2017-04-27T17:06:36-04:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
- tripNumber: `1736` (number) - A sequential number that increases after each trip. Resets after 65,536 trips.
- odometer: `23` (number) - Device-calculated odometer.
- fuelConsumed: `0.03800000086426735` (number) - Fuel consumed during trip in gallons. 
- remaining: `00` (number) - Remaining fuel in the fuel tank in gallons.

### Example

```json
{
    "header": {...},
    "body": {
        "type": "TripEndRecordRelativeTime",
        "timestamp": "2017-04-27T17:06:36-04:00",
        "tripNumber": 1736,
        "odometer": 23,
        "fuelConsumed": 0.03800000086426735,
        "remaining": "00"
    }
}
```

## <a name="trip-end-absolute-time"></a> Trip End Absolute Time

### Example

Currently unavailable

## <a name="trip-end-absolute-time-gps"></a> Trip End Absolute Time and GPS

### Attributes

- type: `TripEndRecordAbsoluteTimeAndGps` (string) - Indicates a type for this event.
- timestamp: `2016-12-08T15:46:21-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
- tripNumber: `39` (number) - A sequential number that increases after each trip. Resets after 65,536 trips.
- odometer: `6` (number) - Device-calculated odometer (see `validity` object for more information).
- gps: (object) - Contains the location where this event was produced.
  - heading: `0` (number) - The angle between the direction in which the object's nose is pointing and a reference direction (e.g. true north).
  - horizontalDilutionOfPrecision: `0` (number) - See [Horizontal Dilution of Precision](../horizontal-dillution-of-precision.md) for more information.
  - latitude: `0` (number)
  - longitude: `0` (number)
  - numberOfSatellites: `0` (number) - Number of satellites used to determine location for this event.
  - hemisphere: `NorthWest` (enum[string]) - The hemisphere of the globe where this event was produced.
    - Members
      - `NorthWest`
      - `NorthEast`
      - `SouthWest`
      - `SouthEast`
  - fixQuality: `NoFix` (enum[string]) - The validity and accuracy of the GPS data.
    - Members
      - `NoFix` - Latitude and longitude are invalid.
      - `Standard` - 2D or 3D fix. Latitude and longitude are valid.
      - `Differential` - Enhanced GPS accuracy.
- fuelConsumed: `0.01899999938905239` (number) - Fuel consumed during trip in gallons. 
- validity: (object) - Additional metadata.
  - gpsRecent: `false` (boolean) 
    - Members
      - `true` - GPS data reported was not cached.
      - `false` - GPS data reported was cached.
  - kmUnits: `false` (boolean) 
    - Members
      - `true` - Device is reporting distance in kilometers
      - `false` - Device is reporting distance in miles.
  - nonObdTripStart: `false` (boolean) 
    - Members
      - `true` - Device detected the trip start while in non-OBD mode.
      - `false` - Device detected the trip start in OBD mode.
  - vehicleOdometer: `false` (boolean) 
    - Members
      - `true` - The odometer value reported above was read from the vehicle.
      - `false` - The odometer value reported above came from the device. This is the expected value for a `TripEnd` event.

### Example

```json
{
  "header": {...},
  "body": {
    "type": "TripEndRecordAbsoluteTimeAndGps",
    "timestamp": "2016-12-08T15:46:21-05:00",
    "tripNumber": 39,
    "odometer": 6,
    "gps": {
      "heading": 0,
      "horizontalDilutionOfPrecision": 0,
      "latitude": 0,
      "longitude": 0,
      "numberOfSatellites": 0,
      "hemisphere": "NorthWest",
      "fixQuality": "NoFix"
    },
    "fuelConsumed": 0.01899999938905239,
    "validity": {
      "gpsRecent": false,
      "kmUnits": false,
      "nonObdTripStart": false,
      "vehicleOdometer": false
    }
  }
}
```
