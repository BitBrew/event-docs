# Trip Event Data by Type

## <a name="accelerometer"></a> AccelerometerEvent

This event represents 1 second of Accelerometer samples. The number of samples per second (Hz) is configurable, so the length of the `eventData` array varies.

### Attributes

- type: `AccelerometerEvent` (string) - The specific type of event.
- relativeSecond: `1` (number) - The relative time from the previous event in seconds.
- eventType: `1` (enum[number]) - Indicates the condition that triggered this event.
  - Members
    - `0` - AT histogram data
    - `1` - Positive X-Axis event
    - `2` - Positive Y-Axis event
    - `4` - Positive Z-Axis event
    - `8` - X histogram data
    - `16` - Negative X-Axis event
    - `32` - Negative Y-Axis event
    - `64` - Negative Z-Axis event
    - `128` - Y Histogram data
    - `136` - Z histogram data
- eventData: (array) - Accelerometer data for this event. The length of the array is equal to the number of samples the device is configured to collect per second (Hz). 24 Hz is the maximum.
  - (object)
    - x: `1` (number) - The X-axis reading
    - y: `0` (number) - The Y-axis reading
    - z: `0` (number) - The Z-axis reading

## <a name="bluetooth"></a> BluetoothEvent

### Attributes

- type: `BluetoothEvent` (string) - The specific type of event.
- bluetoothEventData: (object) - An object that contains the data for this type of event.

### Specific `bluetoothEventData` Types

- TBD

## <a name="fence"></a> FenceEvent

### Attributes

- type: `FenceEvent` (string) - The specific type of event.
- fenceEventData: (object) - An object that contains the data for this type of event.
  - Members
    - TimeFenceEventData: (object) - An object that contains the data for this type of event.
        - startOrEnd: `End` (enum[string])
          - Members:
            - `Start` (number) - Indicates the start of a time fence event.
            - `End` (number) - Inidicates the end of a time fence event.
        - tripNumber: `9` (number) - A sequential number that increases after each trip. Resets after 65,536 trips.
        - distanceTraveledInTimeFence: `15.2`(number) - Distance travelled in miles or kilometers.
        - durationInTimeFence: `7`(number) - Time travelled in minutes.

    - GeoFenceEventData: (object) - An object that contains the data for this type of event.
      - entryOrExit: `Entry` (enum[string])
        - Members:
          - `Entry` - Indicates that the vehicle entered the geofence.
          - `Exit` - Indicates that the vehicle left the geofence.
      - geoFenceId: `1` (number) - An integer representing the geofence in question. Datalogger can be configured with up to 10 geofences.


## <a name="gps"></a> TripGpsEvent

This event type has several subtypes, which provide information about why the event was generated, e.g. after so much time, or so much distance, or because of a change of course over ground (COG). 

There are two examples provided here because the GPS data itself is located in a different object for devices with an Abs. Time and GPS configuration as opposed to an Abs. Time or Relative Time configuration.

### Attributes

- type: `TripGpsEvent` (string) - The specific type of event.
- gpsEventData: (object) - An object that contains the data for this type of event.
  - type: `IgnitionOnPeriodicEvent` (enum[string]) - One of 5 subtypes.
    - Members:
      - `IgnitionOnPeriodicEvent`
      - `CogEvent`
      - `DistanceEvent`
      - `TripStartEvent`
      - `TripEndEvent`
  - gpsData: `4` (number) - Vehicle speed in MPH or KPH. If the value of the `type` field is `TripStartEvent`, this value represents the GPS Fix Quality. `4` represents a valid fix, and `1` represents no fix.
  - gpsRecord: (object)
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

### Example (for Abs. Time and Relative Time Configurations)

This example shows a `TripGpsEvent` for types `TripEventAbsoluteTime` and `TripEventRelativeTime`. For these configurations, the GPS information is provided in the nested `gpsRecord` object.

```json
{
  "header": {...},
  "body": {
    "timestamp": "2017-02-13T15:04:50-05:00",
    "type": "TripEventAbsoluteTime",
    "tripNumber": 46,
    "eventData": {
      "type": "TripGpsEvent",
      "gpsEventData": {
        "type": "IgnitionOnPeriodicEvent",
        "gpsData": 4,
        "gpsRecord": {
          "heading": 132,
          "horizontalDilutionOfPrecision": 0,
          "latitude": 42.28004455566406,
          "longitude": -83.74847412109375,
          "numberOfSatellites": 7,
          "hemisphere": "NorthWest",
          "fixQuality": "Standard"
        },
      }
    }
  }
}
```

### Example (for Abs. Time and GPS Configuration)

This example shows a `TripGpsEvent` for type `TripEventAbsoluteTimeAndGps`. For this configuration, the GPS information is provided in the `gps` object, and not in the nested `gpsRecord` object, whose value is `null`.

```json
{
  "header": {...},
  "body": {
    "timestamp": "2017-06-03T23:14:48-04:00",
    "gps": {
      "heading": 132,
      "horizontalDilutionOfPrecision": 0,
      "latitude": 42.28004455566406,
      "longitude": -83.74847412109375,
      "numberOfSatellites": 7,
      "hemisphere": "NorthWest",
      "fixQuality": "Standard"
    },
    "type": "TripEventAbsoluteTimeAndGps",
    "tripNumber": 46,
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

## <a name="pid"></a> ObdPidEvent

PID Events are often triggered by conditions in the vehicle. This `ObdPidEvent`type has a number of subtypes.

### Attributes

- type: `ObdPidEvent` (string) - The specific type of event.
- pidSize: `2` (number) - The number of bytes in the raw data.
- pidDataType: `MilStatus` (enum[string]) - One of 97 possible PID names.
  - Members
    - `SupportedPids1to32`
    - `MilStatus`
    - `FreezeFrameTroubleCode`
    - `FuelStatus`
    - `CalcEngineLoad`
    - `EngineCoolantTemp`
    - `ShortTermFuelPrctTrimB1`
    - `ShortTermFuelPrctTrimB2`
    - `LongTermFuelPrctTrimB1`
    - `LongTermFuelPrctTrimB2`
    - `FuelPressure`
    - `IntakeManifoldAbsPressure`
    - `EngineRpm`
    - `VehicleSpeed`
    - `TimingAdvance`
    - `IntakeAirTemp`
    - `MafAirFlowRate`
    - `ThrottlePosition`
    - `CommandedSecondaryAirStatus`
    - `OxygenSensorsPresent`
    - `OxygenSensorVoltageB1S1`
    - `OxygenSensorVoltageB1S2`
    - `OxygenSensorVoltageB1S3`
    - `OxygenSensorVoltageB1S4`
    - `OxygenSensorVoltageB2S1`
    - `OxygenSensorVoltageB2S2`
    - `OxygenSensorVoltageB2S3`
    - `OxygenSensorVoltageB2S4`
    - `ObdStandards`
    - `OxygenSensorsPresent2`
    - `AuxiliaryInputStatus`
    - `RunTimeSinceEngineStart`
    - `SupportedPids33to64`
    - `DistanceTraveledMil`
    - `FuelRailPressureRelative`
    - `FuelRailPressure`
    - `OxygenSensor1EquivalenceRatioVoltage`
    - `OxygenSensor2EquivalenceRatioVoltage`
    - `OxygenSensor3EquivalenceRatioVoltage`
    - `OxygenSensor4EquivalenceRatioVoltage`
    - `OxygenSensor5EquivalenceRatioVoltage`
    - `OxygenSensor6EquivalenceRatioVoltage`
    - `OxygenSensor7EquivalenceRatioVoltage`
    - `OxygenSensor8EquivalenceRatioVoltage`
    - `CommandEgr`
    - `EgrError`
    - `CommandEvaporativePurge`
    - `FuelLevelInput`
    - `NumWarmupsSinceCodesCleared`
    - `DistanceTraveledSinceCodesCleared`
    - `EvapSystemVaporPressure`
    - `BarometricPressure`
    - `OxygenSensor1EquivalenceRatioCurrent`
    - `OxygenSensor2EquivalenceRatioCurrent`
    - `OxygenSensor3EquivalenceRatioCurrent`
    - `OxygenSensor4EquivalenceRatioCurrent`
    - `OxygenSensor5EquivalenceRatioCurrent`
    - `OxygenSensor6EquivalenceRatioCurrent`
    - `OxygenSensor7EquivalenceRatioCurrent`
    - `OxygenSensor8EquivalenceRatioCurrent`
    - `CatalystTemperatureBank1Sensor1`
    - `CatalystTemperatureBank1Sensor2`
    - `CatalystTemperatureBank2Sensor1`
    - `CatalystTemperatureBank2Sensor2`
    - `SupportedPids65to96`
    - `MonitorStatusDriveCycle`
    - `ControlModuleVoltage`
    - `AbsoluteLoadValue`
    - `RelativeThrottlePosition`
    - `AmbientAirTemperature`
    - `AbsoluteThrottlePositionB`
    - `AbsoluteThrottlePositionC`
    - `AcceleratorPedalPositionD`
    - `AcceleratorPedalPositionE`
    - `AcceleratorPedalPositionF`
    - `CommandedThrottleActuator`
    - `TimeRunMilOn`
    - `TimeSinceTroubleCodesCleared`
    - `MaxOfErOsvOscMap`
    - `MaxOfMaf`
    - `FuelType`
    - `EthanolFuelPrct`
    - `AbsEvapVaporPressure`
    - `EvapSystemVaporPressure2`
    - `ShortTermSecondaryOxygenSensorTrimBank1AndBank3`
    - `LongTermSecondaryOxygenSensorTrimBank1AndBank3`
    - `ShortTermSecondaryOxygenSensorTrimBank2AndBank4`
    - `LongTermSecondaryOxygenSensorTrimBank2AndBank4`
    - `FuelRailPressureAbs`
    - `RelativeAcceleratorPedalPosition`
    - `HybridBatteryPackLifeRemaining`
    - `EngineOilTemp`
    - `FuelInjectionTiming`
    - `EngineFuelRate`
    - `RawAccelerometer`
    - `NormalizedAccelerometer`
    - `GpsReading`
 - pidData: (*T*) - The data (object, number, string, or boolean) reported by the PID. Structure depends on the `pidDataType`. See [PID Data](pid-data.md) for the expected value associated with each `pidDataType` listed above.

### Example
```json
{
  "header": {...},
  "body": {
    "timestamp": "2017-02-13T15:04:50-05:00",
    "gps": {
      "heading": 132,
      "horizontalDilutionOfPrecision": 0,
      "latitude": 42.28004455566406,
      "longitude": -83.74847412109375,
      "numberOfSatellites": 7,
      "hemisphere": "NorthWest",
      "fixQuality": "Standard"
    },
    "type": "TripEventAbsoluteTimeAndGps",
    "tripNumber": 46,
    "eventData": {
      "type": "ObdPidEvent",
      "pidSize": "2",
      "pidDataType": "MilStatus",
      "pidData": { 
        "commandedOn": true,
        "numCodes": 2,
        "statusSupported": {
        "comprehensiveMonitoringStatus": "true",
        "fuelSystemMonitoringStatus": "true",
        "misfireMonitoringStatus": "true",
        "comprehensiveMonitoringSupported": "false",
        "fuelSystemMonitoringSupported": "true",
        "misfireMonitoringSupported": "false",
        "egrSystemMonitoringStatus1": "true",
        "oxygenSensorHeaterMonitoringStatus1": "false",
        "oxygenSensorMonitoringStatus1": "true",
        "acSystemRefrigerantMonitoringStatus1": "false",
        "secondaryAirSystemMonitoringStatus1": "true",
        "evaporativeSystemMonitoringStatus1": "false",
        "heatedCatalystMonitoringStatus1": "true",
        "catalystMonitoringStatus1": "false",
        "egrSystemMonitoringStatus2": "true",
        "oxygenSensorHeaterMonitoringStatus2": "false",
        "oxygenSensorMonitoringStatus2": "true",
        "acSystemRefrigerantMonitoringStatus2": "false",
        "secondaryAirSystemMonitoringStatus2": "true",
        "evaporativeSystemMonitoringStatus2": "false",
        "heatedCatalystMonitoringStatus2": "true",
        "catalystMonitoringStatus2": "false"
        }
      }
    }
  }
}
```

## <a name="obd-speed-events"></a> ObdSpeedEvent
The `ObdSpeedEvent` type has a number of subtypes.

### Attributes

- type: `ObdSpeedEvent` (string) - The specific type of the event.
- obdSpeedEventData: (object) - An object that contains the data for the `ObdSpeedEvent`. 
  - "type": `Acceleration` (enum[string]) - One of 16 subtypes. Other fields vary respective to each subtype.
    - Members:
      - [`Acceleration`](trip-event-data.md#acceleration)
      - [`AccelerationWithAccelerometerConfirmation`](trip-event-data.md#acceleration-accelerometer-confirmation)
      - [`Braking`](trip-event-data.md#braking)
      - [`BrakingWithAccelerometerConfirmation`](trip-event-data.md#braking-accelerometer-confirmation)
      - [`CumulativeSpeedMetrics`](trip-event-data.md#cumulative-speed-metrics)
      - [`DistanceDrivenInSpeedRange`](trip-event-data.md#distance-in-speed-range)
      - [`DistanceDrivenInTimeRange`](trip-event-data.md#distance-in-time-range)
      - [`Idling`](trip-event-data.md#idling)
      - [`SpeedAccelerationHistogram`](trip-event-data.md#speed-acceleration-histogram)
      - [`SpeedDecelerationHistogram`](trip-event-data.md#speed-deceleration-histogram)
      - [`HighSpeedEventEnd`](trip-event-data.md#high-speed-end)
      - [`HighSpeedEventStart`](trip-event-data.md#high-speed-start)
      - [`TimeDriveninSpeed Range`](trip-event-data.md#time-in-speed-range)
      - [`TimeDriveninTimeRange`](trip-event-data.md#time-in-time-range)
      - [`TripSpeedMetrics`](trip-event-data.md#trip-speed-metrics)
      - [`TripBatteryMetrics`](trip-event-data.md#trip-battery-metrics)


### <a name="acceleration"></a> Acceleration

An acceleration event is generated if the vehicle's acceleration is greater than
or equal to the device's configured `thresholdValue`. The
acceleration event ends when the vehicle's acceleration falls below the
configured `thresholdValue`.


#### Attributes

- obdSpeedEventData: (object)
  - thresholdValue: `25.0` (number) - The configured vehicle speed threshold in MPH/s or KPH/s.
  - maxAcceleration: `6.0` (number) - The actual acceleration that triggered the event in MPH/s or KPH/s.
  - type: `Acceleration` (enum[string]) - Indicates a type for this object.

#### Example

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
        "thresholdValue": 25.0,
        "maxAcceleration": 6.0,
        "type": "Acceleration"
      }
    }
  }
}
```

### <a name="acceleration-accelerometer-confirmation"></a> Acceleration with Accelerometer Confirmation

An acceleration event is generated if the vehicle's acceleration is greater than
or equal to the device's configured `thresholdValue`. The
acceleration event ends when the vehicle's acceleration falls below the
configured `thresholdValue`. This event differs from the Acceleration Event only
in the type, which says that the device's accelerometer has confirmed its veracity. 

The difference between this type and the type above is the confirmation of the device's accelerometer sensor.

#### Attributes

- obdSpeedEventData: (object)
  - thresholdValue: `13.0` (number) - The configured acceleration threshold in MPH/s or KPH/s.
  - maxAcceleration: `6.0` (number) - The actual acceleration (confirmed by the accelerometer in the device) that triggered the event in MPH/s or KPH/s.
  - type: `AccelerationWithAccelerometerConfirmation` (enum[string]) - Indicates a type for this object.

#### Example
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
        "thresholdValue": 13.0,
        "maxAcceleration": 6.0,
        "type": "AccelerationWithAccelerometerConfirmation"
      }
    }
  }
}
```

### <a name="braking"></a> Braking

A braking event is generated if the vehicle's deceleration is greater than or
equal to the device's configured `thresholdValue`. The braking event ends
when the vehicle's deceleration falls below the configured `thresholdValue`.

#### Attributes

- obdSpeedEventData: (object)
  - thresholdValue: `8.0` (number) - The configured deceleration threshold in MPH/s or KPH/s.
  - maxBraking: `6.0` (number) - The actual deceleration that triggered the event in MPH/s or KPH/s.
  - type: `Braking` (enum[string]) - Indicates a type for this object.

#### Example

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
        "thresholdValue": 8.0,
        "maxBraking": 6.0,
        "type": "Braking"
      }
    }
  }
}
```

### <a name="braking-accelerometer-confirmation"></a> Braking with Accelerometer Confirmation

A braking event is generated if the vehicle's deceleration is greater than or
equal to the device's configured `thresholdValue`. The braking event ends
when the vehicle's deceleration falls below the configured `thresholdValue`. This event differs from the Braking Event only
in the type, which says that the device's accelerometer has confirmed its veracity. 

The difference between this type and the type above is the confirmation of the device's accelerometer sensor.

#### Attributes

- obdSpeedEventData: (object)
  - thresholdValue: `25.0` (number) - The configured deceleration threshold in MPH/s or KPH/s.
  - maxValue: `6.0` (number) - The actual deceleration (confirmed by the accelerometer in the device) that triggered the event in MPH/s or KPH/s.
  - type: `BrakingWithAccelerationConfirmation` (enum[string]) - Indicates a type for this object.

#### Example
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
        "thresholdValue": 25.0,
        "maxValue": 6.0,
        "type": "BrakingWithAccelerationConfirmation"
      }
    }
  }
}
```

### <a name="cumulative-speed-metrics"></a> Cumulative Speed Metrics

Cumulative speed metrics provide a running count of certain interesting speed-related metrics since the device was deployed.

#### Attributes

- obdSpeedEventData: (object)
  - hardAccelerationCount: `5` (number) - The total number of hard acceleration events since the device was deployed.
  - hardBrakingCount: `20` (number) - The total number of hard braking events since the device was deployed.
  - totalIdling: `20` (number) - The total number of idling events since the device was deployed.
  - overSpeedCount: `0` (number) - The total number of speeding events since the device was deployed.
  - tripDistance: `8825` (number) - The total distance travelled in miles or kilometers. Units depends on device configuration.
  - overSpeedDistance: `0` (number) - The total distance travelled in miles or kilometers at a velocity greater than the configured speeding threshold.
  - tripTimeHours: `9427` (number) - The total time travelled in hours since the device was deployed.
  - type: `CumulativeSpeedMetrics` (enum[string]) - Indicates a type for this object.

#### Example

```json
{
  "header": {...},
  "body": {
    "type": "TripEventRelativeTime",
    "timestamp": "2016-12-29T11:19:45-05:00",
    "tripNumber": 235,
    "eventData": {
      "type": "ObdSpeedEvent",
      "obdSpeedEventData": {
        "hardAccelerationCount": 5,
        "hardBrakingCount": 20,
        "totalIdling": 250,
        "overSpeedCount": 0,
        "tripDistance": 8825,
        "overSpeedDistance": 0,
        "tripTimeHours": 9427,
        "type": "CumulativeSpeedMetrics"
      }
    }
  }
}
```

### <a name="distance-in-speed-range"></a> Distance Driven in Speed Range

This `obdSpeedEventData` type describes the distance driven (in miles or kilometers based on device
configuration) for a configurable set of speed ranges (in miles per hour or
kilometers per hour based on device configuration).

There are up to 20 configurable speed buckets (excluding the first and last, which are predefined).

The platform is unable to provide the custom definitions for the speed ranges
used in this event type. Please consult the speed range definitions in the
device configuration when using data from this event type.

#### Attributes

- obdSpeedEventData: (object)
  - data: (array[number])
    - Members
      - `0.2` - Distance driven in the first speed bucket, which is zero MPH or KPH.
      - `0.5` - Distance driven in the second speed bucket, which is 1-A (A is a configurable speed in MPH or KPH).
      - `1.3` - Distance driven in the third speed bucket, which is A-B (A and B are a configurable speeds in MPH or KPH).
      - `2.5` - Distance driven in the fourth speed bucket, which is B-C (B and C are a configurable speeds in MPH or KPH).
      - `10.2` - Distance driven in the fifth speed bucket, which is C-D (C and D are a configurable speeds in MPH or KPH).
      - `4.0` - Distance driven in the sixth speed bucket, which is D-E (D and E are a configurable speeds in MPH or KPH).
      - `0.0` - Distance driven in the seventh speed bucket, which is greater than E (E is a configurable speed in MPH or KPH).
  - type: `DistanceDrivenInSpeedRange` (enum[string]) - Indicates a type for this object.

#### Example

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
        "data": [
            0.2,
            0.5,
            1.3,
            2.5,
            10.2,
            4.0,
            0.0
        ],
        "type": "DistanceDrivenInSpeedRange"
      }
    }
  }
}
```

### <a name="distance-in-time-range"></a> Distance Driven in Time Range

This `obdSpeedEventData` type records the distance driven during a trip (in miles or kilometers based on device
configuration) during each hour of the day. The device uses local time (with
Daylight Savings Time when applicable) to record the distance driven in each
time range.

#### Attributes

- obdSpeedEventData (object)
  - data (array[number]) - An array of length 24 where each entry is the number of miles or kilometers (based on device configuration) driven during a trip in each hour-long segment. The time is in local time and includes Daylight Savings Time (when applicable).
    - Members:
      - 0 (number) - Number of miles or kilometers driven between 00:00 and 00:59 (midnight and 12:59 AM).
      - 0 (number) - Number of miles or kilometers driven between 01:00 and 01:59.
      - 0 (number) - Number of miles or kilometers driven between 02:00 and 02:59.
      - 0 (number) - Number of miles or kilometers driven between 03:00 and 03:59.
      - 0 (number) - Number of miles or kilometers driven between 04:00 and 04:59.
      - 0 (number) - Number of miles or kilometers driven between 05:00 and 05:59.
      - 0 (number) - Number of miles or kilometers driven between 06:00 and 06:59.
      - 0 (number) - Number of miles or kilometers driven between 07:00 and 07:59.
      - 0 (number) - Number of miles or kilometers driven between 08:00 and 08:59.
      - 0 (number) - Number of miles or kilometers driven between 09:00 and 09:59.
      - 0 (number) - Number of miles or kilometers driven between 10:00 and 10:59.
      - 0 (number) - Number of miles or kilometers driven between 11:00 and 11:59.
      - 0 (number) - Number of miles or kilometers driven between 12:00 and 12:59.
      - 0 (number) - Number of miles or kilometers driven between 13:00 and 13:59.
      - 0 (number) - Number of miles or kilometers driven between 14:00 and 14:59.
      - 20 (number) - Number of miles or kilometers driven between 15:00 and 15:59.
      - 0 (number) - Number of miles or kilometers driven between 16:00 and 16:59.
      - 0 (number) - Number of miles or kilometers driven between 17:00 and 17:59.
      - 0 (number) - Number of miles or kilometers driven between 18:00 and 18:59.
      - 0 (number) - Number of miles or kilometers driven between 19:00 and 19:59.
      - 0 (number) - Number of miles or kilometers driven between 20:00 and 20:59.
      - 0 (number) - Number of miles or kilometers driven between 21:00 and 21:59.
      - 0 (number) - Number of miles or kilometers driven between 22:00 and 22:59.
      - 0 (number) - Number of miles or kilometers driven between 23:00 and 23:59.
  - type: `DistanceDrivenInTimeRange` (enum[string]) - Indicates a type for this object.

#### Example

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
        "data": [
          0,
          0,
          0,
          0,
          0,
          0,
          0,
          0,
          0,
          0,
          0,
          0,
          0,
          0,
          0,
          20,
          0,
          0,
          0,
          0,
          0,
          0,
          0,
          0
        ],
        "type": "DistanceDrivenInTimeRange"
      }
    }
  }
}
```
### <a name="high-speed-end"></a> High Speed Event End

A `highSpeedEventEnd` event is generated after a `highSpeedEventStart` event if
the vehicle's speed drops below the `thresholdValue` and stays below the
`thresholdValue` for a configurable number of seconds.

#### Attributes

- obdSpeedEventData: (object)
  - thresholdValue: `80.0` (number) - The configured vehicle speed threshold in MPH or KPH.
  - triggeredValue: `83.0` (number) - The actual vehicle speed reading that triggered the event (MPH or KPH).
  - maxSpeed: `85.1` (number)) - The maximum vehicle speed read during this event (MPH or KPH).
  - avgSpeed: `82.3` (number) - The average vehicle speed during this event (MPH or KPH).
  - overSpeedTime: `200` (number) - The time spent over the `thresholdValue` in seconds.
  - overSpeedDistance: `3.5` (number) - The distance travelled while over the `thresholdValue` in miles or kilometers.
  - type: `HighSpeedEventEnd` (enum[string]) - Indicates a type for this object.

#### Example

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
        "thresholdValue": 80.0,
        "triggeredValue": 83.0,
        "maxSpeed": 85.1,
        "avgSpeed": 82.3,
        "overSpeedTime": 200,
        "overSpeedDistance": 3.5,
        "type": "HighSpeedEventEnd"
      }
    }
  }
}
```

### <a name="high-speed-start"></a> High Speed Event Start

A `highSpeedEventStart` event is generated if the vehicle's speed is greater
than or equal to the `thresholdValue` and stays above the `thresholdValue` for a
configurable number of seconds.

When the vehicle's speed drops below the `thresholdValue`, a `highSpeedEventEnd`
event is produced (see above).

#### Attributes

- obdSpeedEventData: (object)
  - thresholdValue: `80.0` (number) - The configured vehicle speed threshold in MPH or KPH.
  - triggeredValue: `80.2` (number) - The actual vehicle speed reading that triggered the event (MPH or KPH).
  - type: `HighSpeedEventStart` (string)

#### Example

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
        "thresholdValue": 80.0,
        "triggeredValue": 80.2,
        "type": "HighSpeedEventStart"
      }
    }
  }
}
```

### <a name="idling"></a> Idling

An idling event is generated if the vehicle's speed is less than or equal to the configured `thresholdValue` for the number of seconds specified in the `duration` field.

#### Attributes

- obdSpeedEventData: (object)
  - thresholdValue: `2.0` (number) - The configured vehicle speed threshold in MPH or KPH.
  - duration: `300` (number) - The configured number of seconds that vehicle speed must be below `thresholdValue`.
  - type: `Idling` (enum[string]) - Indicates a type for this object.

#### Example

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
        "thresholdValue": 2.0,
        "duration": 300,
        "type": "DistanceDrivenInTimeRange"
      }
    }
  }
}
```

### <a name="speed-acceleration-histogram"></a> Speed Acceleration Histogram

This `obdSpeedEventData` type describes the time driven for a configurable set of acceleration ranges (in miles per hour per second or
kilometers per hour second based on device configuration).

There are up to 20 configurable acceleration buckets (excluding the first and last, which are predefined).

The platform is unable to provide the custom definitions for the acceleration ranges
used in this event type. Please consult the acceleration range definitions in the
device configuration when using data from this event type.

#### Attributes

- obdSpeedEventData: (object)
  - data: (array[number])
      - Members
      - `101` - Time in seconds driven in the first acceleration bucket, which is zero MPH/s or KPH/s.
      - `0` - Time driven in the second acceleration bucket, which is 1-A (A is a configurable speed in MPH/s or KPH/s).
      - `0` - Time driven in the third acceleration bucket, which is A-B (A and B are a configurable speeds in MPH/s or KPH/s).
      - `0` - Time driven in the fourth acceleration bucket, which is B-C (B and C are a configurable speeds in MPH/s or KPH/s).
      - `0` - Time driven in the fifth acceleration bucket, which is C-D (C and D are a configurable speeds in MPH/s or KPH/s).
      - `0` - Time driven in the seventh acceleration bucket, which is greater than D (D is a configurable speed in MPH/s or KPH/s).
  - type: `SpeedAccelerationHistogram` (enum[string]) - Indicates a type for this object.

#### Example

```json
{
  "header": {...},
  "body": {
    "type": "TripEventRelativeTime",
    "timestamp": "2017-04-15T11:09:42-05:00",
    "tripNumber": 400,
    "eventData": {
      "type": "ObdSpeedEvent",
      "obdSpeedEventData": {
        "data": [
          101,
          0,
          0,
          0,
          0,
          0
        ],
        "type": "SpeedAccelerationHistogram"
      }
    }
  }
}
```

### <a name="speed-deceleration-histogram"></a> Speed Deceleration Histogram

This `obdSpeedEventData` type describes the time driven for a configurable set of deceleration ranges (in miles per hour per second or
kilometers per hour second based on device configuration).

There are up to 20 configurable deceleration buckets (excluding the first and last, which are predefined).

The platform is unable to provide the custom definitions for the deceleration ranges
used in this event type. Please consult the deceleration range definitions in the
device configuration when using data from this event type.

#### Attributes

- obdSpeedEventData: (object)
  - data: (array[number])
    - Members
    - `189` - Time in seconds driven in the first deceleration bucket, which is zero MPH/s or KPH/s.
    - `400` - Time driven in the second deceleration bucket, which is 1-A (A is a configurable speed in MPH/s or KPH/s).
    - `237` - Time driven in the third deceleration bucket, which is A-B (A and B are a configurable speeds in MPH/s or KPH/s).
    - `15` - Time driven in the fourth deceleration bucket, which is B-C (B and C are a configurable speeds in MPH/s or KPH/s).
    - `3` - Time driven in the fifth deceleration bucket, which is C-D (C and D are a configurable speeds in MPH/s or KPH/s).
    - `0` - Time driven in the seventh deceleration bucket, which is greater than D (D is a configurable speed in MPH/s or KPH/s).
  - type: `SpeedDecelerationHistogram` (enum[string]) - Indicates a type for this object.

#### Example

```json
{
  "header": {...},
  "body": {
    "type": "TripEventRelativeTime",
    "timestamp": "2017-02-28T14:27:10-05:00",
    "tripNumber": 115,
    "eventData": {
      "type": "ObdSpeedEvent",
      "obdSpeedEventData": {
        "data": [
            189,
            400,
            237,
            15,
            3,
            0
        ],
        "type": "SpeedDecelerationHistogram"
      }
    }
  }
}
```

### <a name="time-in-speed-range"></a> Time Driven in Speed Range

This `obdSpeedEventData` type describes the time driven in seconds for a configurable 
set of speed ranges (in miles per hour or kilometers per hour based on device configuration).

There are up to 20 configurable speed buckets (excluding the first and last, which are predefined).

The platform is unable to provide the custom definitions for the speed ranges
used in this event type. Please consult the speed range definitions in the
device configuration when using data from this event type.

#### Attributes

- obdSpeedEventData: (object)
  - data: (array[number])
    - Members
      - `62` - Time in seconds driven in the first speed bucket, which is zero MPH or KPH.
      - `142` - Time in seconds driven in the second speed bucket, which is 1-A (A is a configurable speed in MPH or KPH).
      - `95` - Time in seconds driven in the third speed bucket, which is A-B (A and B are a configurable speeds in MPH or KPH).
      - `20` - Time in seconds driven in the fourth speed bucket, which is B-C (B and C are a configurable speeds in MPH or KPH).
      - `0` - Time in seconds driven in the fifth speed bucket, which is C-D (C and D are a configurable speeds in MPH or KPH).
      - `0` - Time in seconds driven in the sixth speed bucket, which is D-E (D and E are a configurable speeds in MPH or KPH).
      - `0` - Time in seconds driven in the seventh speed bucket, which is greater than E (E is a configurable speed in MPH or KPH).
  - type: `TimeDrivenInSpeedRange` (enum[string]) - Indicates a type for this object.

#### Example

```json
{
  "obdSpeedEventData": {
      "data": [
          62,
          142,
          95,
          20,
          0,
          0,
          0
      ],
      "type": "TimeDrivenInSpeedRange"
  }
}
```

### <a name="time-in-time-range"></a> Time Driven in Time Range

Describes the time driven (seconds) during each hour of the day. The device uses
local time (with Daylight Savings Time when applicable) to record the time
driven in each time range. If a device moves time zones, the event reports 
from the time zone the trip began in.

#### Attributes

- obdSpeedEventData: (object)
  - data: (array[number]) - An array of length 24 where each entry is the number of seconds driven during each hour. The time is in local time and includes Daylight Savings Time (when applicable).
    - Members
      - 0 (number) - Number of seconds driven between 00:00 and 00:59 (midnight and 12:59 AM).
      - 0 (number) - Number of seconds driven between 01:00 and 01:59.
      - 0 (number) - Number of seconds driven between 02:00 and 02:59.
      - 0 (number) - Number of seconds driven between 03:00 and 03:59.
      - 0 (number) - Number of seconds driven between 04:00 and 04:59.
      - 0 (number) - Number of seconds driven between 05:00 and 05:59.
      - 0 (number) - Number of seconds driven between 06:00 and 06:59.
      - 0 (number) - Number of seconds driven between 07:00 and 07:59.
      - 0 (number) - Number of seconds driven between 08:00 and 08:59.
      - 0 (number) - Number of seconds driven between 09:00 and 09:59.
      - 0 (number) - Number of seconds driven between 10:00 and 10:59.
      - 0 (number) - Number of seconds driven between 11:00 and 11:59.
      - 0 (number) - Number of seconds driven between 12:00 and 12:59.
      - 0 (number) - Number of seconds driven between 13:00 and 13:59.
      - 0 (number) - Number of seconds driven between 14:00 and 14:59.
      - 235 (number) - Number of seconds driven between 15:00 and 15:59.
      - 0 (number) - Number of seconds driven between 16:00 and 16:59.
      - 0 (number) - Number of seconds driven between 17:00 and 17:59.
      - 0 (number) - Number of seconds driven between 18:00 and 18:59.
      - 0 (number) - Number of seconds driven between 19:00 and 19:59.
      - 0 (number) - Number of seconds driven between 20:00 and 20:59.
      - 0 (number) - Number of seconds driven between 21:00 and 21:59.
      - 0 (number) - Number of seconds driven between 22:00 and 22:59.
      - 0 (number) - Number of seconds driven between 23:00 and 23:59.
  - type: `TimeDrivenInTimeRange` (enum[string]) - Indicates a type for this object.

#### Example

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
        "data": [
          0,
          0,
          0,
          0,
          0,
          0,
          0,
          0,
          0,
          0,
          0,
          0,
          0,
          0,
          0,
          235,
          0,
          0,
          0,
          0,
          0,
          0,
          0,
          0
        ],
        "type": "TimeDrivenInTimeRange"
          }
        }
      }
    }
```

### <a name="trip-speed-metrics"></a> Trip Speed Metrics

Trip speed metrics provide a snapshot of certain interesting speed-related metrics. This event is sent at the end of a trip.

#### Attributes

- obdSpeedEventData: (object)
  - hardAccelerationCount: `0` (number) - The total number of hard acceleration events during the trip.
  - hardBrakingCount: `0` (number) - The total number of hard braking events during the trip.
  - totalIdling: `0` (number) - The total number of idling events during the trip.
  - overSpeedCount: `0` (number) - The total number of speeding events during the trip.
  - tripDistance: `0.10000000149011612` (number) - The total distance travelled during the trip in miles or kilometers. Units depends on device configuration.
  - averageDriveSpeed: `6.199999809265137` (number) - The average vehicle speed in MPH or KMH during the trip. Units depends on device configuration.
  - overSpeedDistance: `0` (number)- The total distance travelled in miles or kilometers at a velocity greater than the configured speeding threshold. Units depends on device configuration.
  - maxSpeed: `6.199999809265137` (number) - The maximum vehicle speed recorded during the trip.
  - tripTimeSeconds: `105` (number) - The duration of the trip in seconds.
  - type: `SpeedMetricsPerTrip` (enum[string]) - Indicates a type for this object.


#### Example

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
        "hardAccelerationCount": 0,
        "hardBrakingCount": 0,
        "totalIdling": 0,
        "overSpeedCount": 0,
        "tripDistance": 0.10000000149011612,
        "averageDriveSpeed": 6.199999809265137,
        "overSpeedDistance": 0,
        "maxSpeed": 6.199999809265137,
        "tripTimeSeconds": 105,
        "type": "SpeedMetricsPerTrip"
          }
        }
      }
    }
```

### <a name="trip-battery-metrics"></a> Trip Battery Metrics

Battery metrics during the trip.

#### Attributes

- obdSpeedEventData: (object)
  - engineTimeToStart: `42` (number) - The time it took the engine to start in milliseconds. 
  - averageInTripVoltage: `12.199999809265137` (number) - The average battery voltage during the trip.
  - minimumBatteryVoltage: `12` (number) - The minimum battery voltage. This value almost always reflects the battery voltage during crank (key-on).
  - restingVoltage: `12` (number) - The resting voltage of the battery. This value was collected at a configured interval after the previous trip end.
   - type: `BatteryMetricsPerTrip` (enum[string]) - Indicates a type for this event.

#### Example

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
        "restingVoltage": 12
        "type": "BatteryMetricsPerTrip"
          }
        }
      }
    }
```
