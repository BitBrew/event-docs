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

## Events

### Broker Type Name

The name of this broker type is `DanlawUdp`.

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
