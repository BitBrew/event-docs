# Danlaw UDP Broker Events

The Danlaw UDP broker supports devices that send UDP messages using the Danlaw
UDP protocol. Messages for the Danlaw UDP protocol are converted to platform
events.

## Messages

The Danlaw UDP protocol consists of a communication flow and binary data
encoding. The broker is responsible for handling the communication flow and data
decoding.

Danlaw devices pack data into a compact binary encoding. A single datagram
typically contains data for multiple platform events. The datagram format is
depicted in the following sections.

### Packet Composition

A packet is responsible for identifying and coordinating device to platform
communication. It lives inside a
[datagram](https://en.wikipedia.org/wiki/User_Datagram_Protocol), and wraps one
or more messages.

| Packet Component       | Description                                  |
| ---------------------- | -------------------------------------------- |
| Packet Header          | Contains device IDs, payload size, etc.      |
| Messages 1 - N         | A collection of messages (see table below)   |
| Packet Footer          | Checksum for the packet contents             |

### Message Composition

Messages deliver data about something that occurred on the device or in the
vehicle. Messages produce platform events.

| Message Component      | Description                                  |
| ---------------------- | -------------------------------------------- |
| Message Header         | Contains message type, time, location, etc.  |
| Message Body           | Contains the data for this message type      |
| Message Footer         | Contains a checksum for the message contents |

Events sent over the UDP protocol therefore contain two headers: the platform-appended header discussed [here](events-overview.md#platform-header) and the header referenced in the table above.

## Events

### Broker Type Name

The name of this broker type is `DanlawUdp`.

### Event Header
This header—its format and fields—is specific to the UDP protocol, and is not the same as the [platform-appended header](events-overview.md#platform-header) which appears on every event regardless of protocol.

#### Attributes

- header (object)
  - timestamp: `2016-02-05T10:36:31-05:00` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the event was produced on the device.
  - latitude: `42.2793934` (number)
  - tripType: `Trip`(enum[string]) - Indicates a contextual type for this event.
    - Members
      - `IgnitionOff`
      - `Trip`
      - `Idling`
      - `Unknown`
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
  - longitude: `-83.72955975` (number)
  - messageType: `10` (number) - 
  - odo: `22` (number) - Vehicle odometer or device-calculated odometer.
  - tripNumber: `23`- A sequential number that increases after each trip. Resets after 65,536 trips.
  - fixQuality: `FixInvalid` (enum[string]) - The validity and accuracy of the GPS data.
    - Members
      - `FixOk` - 2D or 3D fix. Latitude and longitude are valid.
      - `StoredFix` - Latitude and longitude are readings from (up to) 5 seconds ago, because the device has not been able to get a GPS fix for 5 seconds.
      - `FixInvalid` - Latitude and longitude are invalid.
      - `Unknown` - The platform cannot decode the value.
  - messageLength: `6`(number) - Indicates the total bytes of the message, including the checksum.

#### Example

```
    "header": {
      "timestamp": "2016-02-05T10:36:31-05:00",
      "latitude": 0.0,
      "tripType": "Trip",
      "vehicleProtocolId": "ISO15765_11_BIT_CAN",
      "longitude": 0.0,
      "messageType": 10,
      "odo": 22,
      "tripNumber": 23,
      "fixQuality": "FixInvalid",
      "messageLength": 6
    }
```

### Event Types

- [Accelerometer](danlawudp-events/accelerometer.md)
- [Bluetooth Beacon](danlawudp-events/bluetooth-beacon.md)
- [Bluetooth FOB](danlawudp-events/bluetooth-fob.md)
- [Device Connect](danlawudp-events/device-connect.md)
- [Device Disconnect](danlawudp-events/device-disconnect.md)
- [Device Health](danlawudp-events/device-health.md)
- [First Plugin](danlawudp-events/first-plugin.md)
- [Fuel Level Change](danlawudp-events/fuel-level-change.md)
- [Geo Fence](danlawudp-events/geo-fence.md)
- [GPS](danlawudp-events/gps.md)
- [Hard Acceleration](danlawudp-events/hard-acceleration.md)
- [Hard Brake](danlawudp-events/hard-brake.md)
- [Idling](danlawudp-events/idling.md)
- [IO Extender](danlawudp-events/io-extender.md)
- [OBD](danlawudp-events/obd.md)
- [Speeding](danlawudp-events/speeding.md)
- [Power Take Off](danlawudp-events/power-take-off.md)
- [Real Time Disconnect](danlawudp-events/real-time-disconnect.md)
- [Time Fence](danlawudp-events/time-fence.md)
- [Trip End](danlawudp-events/trip-end.md)
- [Trip Start](danlawudp-events/trip-start.md)
- [Vehicle Battery](danlawudp-events/vehicle-battery.md)
- [Vehicle DTCs - Current](danlawudp-events/vehicle-dtcs-current.md)
- [Vehicle DTCs - Pending](danlawudp-events/vehicle-dtcs-pending.md)
- [Vehicle Function Signal](danlawudp-events/vehicle-function-signal.md)
- [Vehicle MIL](danlawudp-events/vehicle-mil.md)
- [Vehicle Movement](danlawudp-events/vehicle-movement.md)
- [VIN Change](danlawudp-events/vin-change.md)
