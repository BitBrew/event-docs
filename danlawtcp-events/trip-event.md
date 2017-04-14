# Trip Event

## <a name="trip-event-relative-time"></a> Trip Event Relative Time

### Attributes 

- type: `TripEventRelativeTime` (string) - Indicates a type for this object.
- timestamp: `2016-12-08T15:46:21-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
- tripNumber: `5` (number) - A sequential number that increases after each trip. Resets after 65,536 trips.
- eventData (object) - Contains data for a trip event.
  - type: `ObdSpeedEvent` (enum[string]) - One of 6 possible event types. Other properties in this object vary respective to the type.
    - Members:
      - [`AccelerometerEvent`](trip-event-data.md#accelerometer)
      - [`BluetoothEvent`](trip-event-data.md#bluetooth)
      - [`FenceEvent`](trip-event-data.md#fence)
      - [`TripGpsEvent`](trip-event-data.md#gps)
      - [`ObdPidEvent`](trip-event-data.md#pid)
      - [`ObdSpeedEvent`](trip-event-data.md#obd-speed-events)

### Example

```json
{
  "header": {...},
  "body": {
    "type": "TripEventRelativeTime",
    "timestamp": "2016-12-29T11:19:45-05:00",
    "tripNumber": 5,
    "eventData": {
      "type": "ObdSpeedEvent",
      "obdSpeedEventData": {
        "engineTimeToStart": 42,
        "averageInTripVoltage": 12.199999809265137,
        "minimumBatteryVoltage": 12,
        "restingVoltage": 12,
        "type": "BatteryMetricsPerTrip"
      }
    }
  }
}
```
## <a name="trip-event-absolute-time"></a> Trip Event Absolute Time

### Attributes

- type: `TripEventAbsoluteTime` (string) - Indicates a type for this object.
- timestamp: `2016-12-08T15:46:21-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
- tripNumber: `39` (number) - A sequential number that increases after each trip.
- eventData (object) - Contains data for a trip event.
  - type: `ObdSpeedEvent` (enum[string]) - One of 6 possible event types. Other properties in this object vary respective to the type.
    - Members:
      - [`AccelerometerEvent`](trip-event-data.md#accelerometer)
      - [`BluetoothEvent`](trip-event-data.md#bluetooth)
      - [`FenceEvent`](trip-event-data.md#fence)
      - [`TripGpsEvent`](trip-event-data.md#gps)
      - [`ObdPidEvent`](trip-event-data.md#pid)
      - [`ObdSpeedEvent`](trip-event-data.md#obd-speed-events)

### Example

```json
{
  "header": {...},
  "body": {
    "type": "TripEventAbsoluteTime",
    "timestamp": "2016-12-08T15:46:21-05:00",
    "tripNumber": 39,
    "eventData": {
      "type": "ObdSpeedEvent",
      "obdSpeedEventData": {
        "engineTimeToStart": 42,
        "averageInTripVoltage": 12.199999809265137,
        "minimumBatteryVoltage": 12,
        "restingVoltage": 12,
        "type": "BatteryMetricsPerTrip"
      }
    }
  }
}
```
## <a name="trip-event-absolute-time-gps"></a> Trip Event Absolute Time and GPS
For devices configured for Absolute Time and GPS, every trip event contains a GPS object.

### Attributes

- type: `TripEventAbsoluteTimeAndGps` (string) - Indicates a type for this object.
- timestamp: `2017-02-13T15:06:34-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
- tripNumber: `46` (number) - A sequential number that increases after each trip.
- gps: (object) - Contains the location where this event was produced.
  - heading: `132` (number) - The angle between the direction in which the object's nose is pointing and a reference direction (e.g. true north).
  - horizontalDilutionOfPrecision: `1` (number) - See [Horizontal Dilution of Precision](../horizontal-dillution-of-precision.md) for more information.
  - latitude: `42.28004455566406` (number)
  - longitude: `-83.74847412109375` (number)
  - numberOfSatellites: `7` (number) - How many satellites the device is tracking for GPS.
  - hemisphere: `NorthWest` (enum[string])
    - Members
      - `NorthWest`
      - `NorthEast`
      - `SouthWest`
      - `SouthEast`
  - fixQuality: `Standard` (enum[string]) - Determines the validity and accuracy of the GPS data.
    - Members
      - `NoFix` - Latitude and longitude are invalid.
      - `Standard` - 2D or 3D fix. Latitude and longitude are valid.
      - `Differential` - Enhanced GPS accuracy.
- eventData (object) - Contains data for a trip event.
  - type: `ObdSpeedEvent` (enum[string]) - One of 6 possible event types. Other properties in this object vary respective to the type.
    - Members:
      - [`AccelerometerEvent`](trip-event-data.md#accelerometer)
      - [`BluetoothEvent`](trip-event-data.md#bluetooth)
      - [`FenceEvent`](trip-event-data.md#fence)
      - [`TripGpsEvent`](trip-event-data.md#gps)
      - [`ObdPidEvent`](trip-event-data.md#pid)
      - [`ObdSpeedEvent`](trip-event-data.md#obd-speed-events)

### Example

```json
{
  "header": {...},
  "body": {
    "type": "TripEventAbsoluteTimeAndGps",
    "timestamp": "2017-02-13T15:04:50-05:00",
    "tripNumber": 46,
    "gps": {
      "heading": 132,
      "horizontalDilutionOfPrecision": 0,
      "latitude": 42.28004455566406,
      "longitude": -83.74847412109375,
      "numberOfSatellites": 7,
      "hemisphere": "NorthWest",
      "fixQuality": "Standard"
    },
    "eventData": {
      "type": "TripGpsEvent",
      "gpsEventData": {
        "type": "IgnitionOnPeriodicEvent",
        "gpsData": 4,
        "gpsRecord": null
      }
    }
  }
}
```
