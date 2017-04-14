# Trip Start

## <a name="trip-start-relative-time"></a> Trip Start Relative Time

### Attributes

- timestamp: `2017-02-13T15:06:34-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
- odometer: `8600` (number) - Vehicle odometer or device-calculated odometer.
- obdSupportedPids: (object) - A map of PID names to boolean. True means the vehicle can provide data for this PID to the device. See the example for the list of PID names.
- vehicleProtocol: `CAN11Bit` (enum[string]) - The type of protocol the device detected on the vehicle bus.
  - Members
    - `VPW1`
    - `PWM`
    - `ISO9141`
    - `ISO14230`
    - `ISO14230FastInit`
    - `CAN11Bit`
    - `CAN29Bit`
- pidList: (array[number]) - List of PIDs that the device is configured to collect data from during a trip.
- vin: `2FTZF1864WCB87930` (string) - Vehicle Identification Number provided by the vehicle. Empty string when VIN is unavailable.
- type: `TripStartRelativeTime` (enum[string]) - Indicates a type for this object.
- tripNumber: `3` (number) - A sequential number that increases after each trip. Resets after 65,536 trips.

### Example

```json
{
  "header": {...},
  "body": {
    "timestamp": "2017-02-13T15:06:34-05:00",
    "odometer": 8600,
    "obdSupportedPids": {
      "O2S7EquivalenceRatioVolts": false,
      "O2S4EquivalenceRatioVolts": false,
      "EngineCoolantTemp": true,
      "MonitorStatusDriveCycle": true,
      "EngineRpm": true,
      "CatalystTempB1S1": true,
      "AcceleratorPedalPositionE": true,
      "Blank1": false,
      "B2S2OxygenSensorVoltageShortTermFuelTrim": true,
      "IntakeAirTemp": true,
      "B2S1OxygenSensorVoltageShortTermFuelTrim": true,
      "O2S5EquivalenceRatioVolts": false,
      "ControlModuleVoltage": true,
      "TimingAdvance": true,
      "FuelType": true,
      "O2S6EquivalenceRatioCurrent": false,
      "O2S3EquivalenceRatioCurrent": false,
      "EvapSystemVaporPressure": false,
      "CommandEgr": false,
      "B1S4OxygenSensorVoltageShortTermFuelTrim": true,
      "B1S1OxygenSensorVoltageShortTermFuelTrim": true,
      "O2S8EquivalenceRatioCurrent": false,
      "MaxOfMaf": false,
      "FuelRailPressure": true,
      "BarometricPressure": true,
      "CatalystTempB1S2": false,
      "AcceleratorPedalPositionF": false,
      "O2S1EquivalenceRatioVolts": false,
      "PidsSupported65_96": true,
      "RunTimeSinceEngineStart": true,
      "MilStatus": true,
      "HybridBatteryPackLifeRemaining": false,
      "OxygenSensorsPresent2": true,
      "NumWarmupsSinceCodesCleared": true,
      "Blank2": true,
      "AmbientAirTemperature": true,
      "EngineFuelRate": false,
      "DistanceTraveledSinceCodesCleared": true,
      "CommandEquivalenceRatio": true,
      "ObdStandards": true,
      "B2S4OxygenSensorVoltageShortTermFuelTrim": true,
      "RelativeAcceleratorPedalPosition": false,
      "LongTermSecondaryOxygenSensorTrimB2B4": true,
      "EngineOilTemp": false,
      "B1S2OxygenSensorVoltageShortTermFuelTrim": true,
      "FuelRailPressureRelative": false,
      "O2S1EquivalenceRatioCurrent": true,
      "EthanolFuelPrct": false,
      "O2S7EquivalenceRatioCurrent": false,
      "FreezeDtc": true,
      "B1S3OxygenSensorVoltageShortTermFuelTrim": true,
      "B2S3OxygenSensorVoltageShortTermFuelTrim": true,
      "O2S2EquivalenceRatioCurrent": false,
      "ThrottlePosition": true,
      "CommandedSecondaryAirStatus": true,
      "MaxOfErOsvOscMap": false,
      "O2S2EquivalenceRatioVolts": false,
      "OxygenSensorsPresent": true,
      "O2S4EquivalenceRatioCurrent": false,
      "O2S8EquivalenceRatioVolts": false,
      "CalcEngineLoad": true,
      "LongTermFuelPrctB1": true,
      "O2S5EquivalenceRatioCurrent": true,
      "ShortTermSecondaryOxygenSensorTrimB1B3": false,
      "RelativeThrottlePosition": true,
      "FuelLevelInput": false,
      "CatalystTempB2S1": true,
      "PidsSupported33_64": true,
      "AbsoluteLoadValue": true,
      "MafAirFlowRate": true,
      "AuxiliaryInputStatus": true,
      "FuelInjectionTiming": false,
      "AbsEvapVaporPressure": false,
      "ShortTermSecondaryOxygenSensorTrimB2B4": false,
      "EvapVaporPressure": false,
      "FuelRailPressureAbs": false,
      "CommandThrottleActuator": true,
      "ShortTermFuelPrctB2": true,
      "LongTermSecondaryOxygenSensorTrimB1B3": true,
      "ShortTermFuelPrctB1": true,
      "LongTermFuelPrctB2": true,
      "O2S6EquivalenceRatioVolts": false,
      "AbsoluteThrottlePositionC": false,
      "DistanceTraveledMil": true,
      "CatalystTempB2S2": false,
      "TimeRunMilOn": false,
      "IntakeManifoldAbsPressure": true,
      "TimeSinceTroubleCodesCleared": false,
      "CommandedEvaporativePurge": true,
      "FuelStatus": true,
      "AcceleratorPedalPositionD": true,
      "O2S3EquivalenceRatioVolts": false,
      "VehicleSpeed": true,
      "EgrError": false,
      "FuelPressure": true,
      "AbsoluteThrottlePositionB": true
    },
    "vehicleProtocol": "CAN11Bit",
    "pidList": [
      13,
      12,
      128,
      131
    ],
    "vin": "2FTZF1864WCB87930",
    "type": "TripStartRelativeTime",
    "tripNumber": 3
  }
}
```

## <a name="trip-start-absolute-time"></a> Trip Start Absolute Time

### Attributes

- timestamp: `2017-02-13T15:06:34-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
- odometer: `8` (number) - Vehicle odometer or device-calculated odometer (see `validity` object for differentiator).
- validity: (object) - Additional metadata.
  - gpsRecent: `true` (boolean) - This field has no meaning because GPS information is not provided.
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
      - `true` - The odometer reported above was read from the vehicle.
      - `false` - The odometer reported above was calculated by the device.
- type: `TripStartAbsoluteTime` (enum[string]) - Indicates a type for this object.
- tripNumber: `821` (number) - A sequential number that increases after each trip. Resets after 65,536 trips.

### Example

```json
{
  "header": {...},
  "body": {
    "timestamp": "2017-02-13T15:04:49-05:00",
    "odometer": 8,
    "vehicleProtocol": "CAN11Bit",
    "validity": {
      "gpsRecent": true,
      "kmUnits": false,
      "nonObdTripStart": false,
      "vehicleOdometer": false
    },
    "type": "TripStartAbsoluteTime",
    "tripNumber": 821
  }
}
```

## <a name="trip-start-absolute-time-gps"></a> Trip Start Absolute Time and GPS

### Attributes

- timestamp: `2017-02-13T15:06:34-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
- odometer: `8` (number) - Vehicle odometer or device-calculated odometer (see `validity` object for differentiator).
- gps: (object) - Contains the location where this event was produced.
  - heading: `132` (number) - The angle between the direction in which the object's nose is pointing and a reference direction (e.g. true north).
  - horizontalDilutionOfPrecision: `0` (number) - See [Horizontal Dilution of Precision](../horizontal-dillution-of-precision.md) for more information.
  - latitude: `42.28004455566406` (number)
  - longitude: `-83.74847412109375` (number)
  - numberOfSatellites: `7` (number) - Number of satellites used to determine location for this event.
  - hemisphere: `NorthWest` (enum[string]) - The hemisphere of the globe where this event was produced.
    - Members
      - `NorthWest`
      - `NorthEast`
      - `SouthWest`
      - `SouthEast`
  - fixQuality: `Standard` (enum[string]) - The validity and accuracy of the GPS data.
    - Members
      - `NoFix` - Latitude and longitude are invalid.
      - `Standard` - 2D or 3D fix. Latitude and longitude are valid.
      - `Differential` - Enhanced GPS accuracy.
- validity: (object) - Additional metadata.
  - gpsRecent: `true` (boolean) 
    - Members
      - `true` - GPS data reported above was gathered at the time shown on the time stamp.
      - `false` - GPS data reported above is a reading from (up to) 5 seconds ago, because the device has not been able to get a GPS fix for 5 seconds.
  - kmUnits: `false` (boolean) 
    - Members
      - `true` - Device is reporting distance in kilometers.
      - `false` - Device is reporting distance in miles.
  - nonObdTripStart: `false` (boolean) 
    - Members
      - `true` - Device detected the trip start while in non-OBD mode.
      - `false` - Device detected the trip start in OBD mode.
  - vehicleOdometer: `false` (boolean) 
    - Members
      - `true` - The odometer reported above was read from the vehicle.
      - `false` - The odometer reported above was calculated by the device.
- type: `TripStartAbsoluteTimeAndGps` (enum[string]) - Indicates a type for this object.
- tripNumber: `46` (number) - A sequential number that increases after each trip. Resets after 65,536 trips.

### Example

```json
{
  "header": {...},
  "body": {
    "timestamp": "2017-02-13T15:04:49-05:00",
    "odometer": 8,
    "gps": {
      "heading": 132,
      "horizontalDilutionOfPrecision": 0,
      "latitude": 42.28004455566406,
      "longitude": -83.74847412109375,
      "numberOfSatellites": 7,
      "hemisphere": "NorthWest",
      "fixQuality": "Standard"
    },
    "vehicleProtocol": "CAN11Bit",
    "validity": {
      "gpsRecent": true,
      "kmUnits": false,
      "nonObdTripStart": false,
      "vehicleOdometer": false
    },
    "type": "TripStartAbsoluteTimeAndGps",
    "tripNumber": 46
  }
}
```
