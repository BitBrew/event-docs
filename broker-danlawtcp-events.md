# Danlaw TCP Broker Events

The Danlaw TCP broker supports devices that connect to the platform using a TCP
connection and communicate using the Danlaw TCP protocol.

## Datalogger Messages

Datalogger devices are highly configurable, and provide rich data, but their
message structure is complex. Message structure varies based on device
configuration. The corresponding platform events use a structure similar to
Datalogger device messages.

A device can be configured to send data with relative timestamps, absolute
timestamps, or absolute timestamps and GPS information. These different
configurations may increase or decrease the size of data that is sent
from the device to the platform.

The general properties of each configuration are listed below.

| Configuration         | Description                                          |
| --------------------- | ---------------------------------------------------- |
| Relative Time         | TCP data begins with a trip start message that contains an absolute timestamp. All messages that follow contain an integer offset from the previous message. The platform produces an absolute timestamp for each message by applying a message's offset to the previous message's calculated timestamp. |
| Absolute Time         | Each device message contains an absolute timestamp. |
| Absolute Time and GPS | Each device message contains an absolute timestamp and a GPS record. |

The choice of configurations above affects the properties inside device messages.
The table below broadly compares the properties of all messages for each configuration.
Some event types are exceptions.

| Configuration         | Device Timestamp | Local Timezone |        GPS       | PID Based Configuration** |
| --------------------- |:----------------:|:--------------:|:----------------:|:-------------------------:|
| Relative Time         |                  |                |         *        |             x             |
| Absolute Time         |         x        |        x       |         *        |                           |
| Absolute Time and GPS |         x        |        x       |         x        |        <span><span/>      |

\* Only certain message types contain GPS data.<br />
\*\* An OBD-II PID (Parameter ID) is a code used to request data from a vehicle.

## Danlaw TCP Data Collection and Transmission

The Datalogger generates messages internally, connects to the server, and sends
its messages in batches.

The frequency at which the device collects data is configurable for most data
types.

The frequency for message transmission is also configurable. Some configurations
will only transmit data at the end of a trip. Some configurations will
incrementally transmit data during a trip.

## Events

### Broker Type Name

The name of this broker type is `DanlawTcp`.

### Event Hierarchy

#### Trip Start

Trip Start events are generated when a vehicle starts. The trigger for the trip
start is typically related to a drop in voltage on the DLC, followed by engine
RPM readings greater than zero. Devices in a non-OBD mode can detect a trip
start using the accelerometer and GPS.

- [Trip Start Relative Time](danlawtcp-events/trip-start.md#trip-start-relative-time)
- [Trip Start Absolute Time](danlawtcp-events/trip-start.md#trip-start-absolute-time)
- [Trip Start Absolute Time and GPS](danlawtcp-events/trip-start.md#trip-start-absolute-time-gps)

#### Trip Data (Only Produced by Devices With Relative Time Configurations)

Trip data provides [OBD-II PID](https://en.wikipedia.org/wiki/OBD-II_PIDs)
readings at  configurable intervals or triggers.

- [Trip Data](danlawtcp-events/trip-data.md)

#### Trip Events

Trip events are produced when specific conditions are met in the vehicle. Hard
Braking, Hard Acceleration, and Idling are examples of Trip Events.

- [Trip Event Relative Time](danlawtcp-events/trip-event.md#trip-event-relative-time)
- [Trip Event Absolute Time](danlawtcp-events/trip-event.md#trip-event-absolute-time)
- [Trip Event Absolute Time and GPS](danlawtcp-events/trip-event.md#trip-event-absolute-time-gps)

#### Trip End

Trip End events are typically triggered when engine RPMs drop to zero. Devices
in non-OBD mode produce a Trip End event when GPS position is relatively static.

- [Trip End Relative Time](danlawtcp-events/trip-end.md#trip-end-relative-time)
- [Trip End Absolute Time](danlawtcp-events/trip-end.md#trip-end-absolute-time)
- [Trip End Absolute Time and GPS](danlawtcp-events/trip-end.md#trip-end-absolute-time-gps)

#### Device Communication

Device Communication events are exclusive to the TCP protocol, and typically
consist of responses to platform commands.

- [Device Connected](danlawtcp-events/communication.md#device-connected)
- [Data Upload Completed](danlawtcp-events/communication.md#data-upload-completed)
- [Update Command Confirmed](danlawtcp-events/communication.md#update-command-confirmed)
