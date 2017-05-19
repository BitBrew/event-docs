# Events

This document explains connected vehicle events and event types for the platform.

## Overview

An event is a set of data points (sensor readings) that occurred at a specific
time.

The type of sensor readings in an event typically define the type of an event.
For example, a DTC Event has diagnostic trouble codes read from the vehicle's
ECU. A DTC event is different from a Hard Braking Event because the Hard Braking
event contains sensor readings for speed and acceleration, not diagnostic
trouble codes.

Sometimes two types of events have the same types of sensor readings and are
only distinguished by a separate type indicator. For example, a Connect Event is
indistinguishable from a Disconnect Event except for a property that says
whether the event was triggered by a device connection or a device
disconnection.

## Broker Types

Brokers are self-contained communication handlers and data encoders and decoders
for specific devices and/or protocols.

Different types of devices may produce different events. Some devices may
produce overlapping event types.

Somewhere at the intersection of all device types is a common set of events that
all connected vehicle devices should provide. We call this common set of events
the "Core Events." Other types of events are considered "Broker Specific
Events."

## Event Header

All platform events contain a header that contains metadata. The event header
contains a device identifier, broker type, tenant name, message
identifier, an ingestion timestamp and tag collection. The metadata is provided
to help route and correlate events using rules and application logic.

- tags: (array[string]) - A collection of tags that were assigned to the device sending this event.
- messageId: `4440b830-f226-11e6-a9ef-19403a4f36d6` (string) - Unique identifier for the device message that produced the event.
- brokerType: `DanlawUdp` (string) - Name of the broker type that produced the event.
- ingestionTimestamp: `2017-02-13T19:54:44.915Z` (string) - [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted time stamp showing when the message was ingested.
- tenantId: `bitbrew` (string) - Unique identifier of tenant.
- deviceId: `4120572504` (string) - Unique identifier of the device that created the event.

### Example Event Header

The following is an example of a platform event header.

```json
{
    "header": {
        "tags": [
            "fulltracking"
        ],
        "messageId": "4440b830-f226-11e6-a9ef-19403a4f36d6",
        "brokerType": "DanlawUdp",
        "ingestionTimestamp": "2017-02-13T19:54:44.915Z",
        "tenantId": "bitbrew",
        "deviceId": "6020981915"
    },
    "body": {...}
}
```

## Broker Specific Events

The following links describe the broker-specific events available from the
platform.

- [DanlawTCP](broker-danlawtcp-events.md)
- [DanlawUDP](broker-danlawudp-events.md)
- [HTTP](broker-http-events.md)
