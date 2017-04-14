# HTTP Broker Events

The HTTP broker supports devices that send JSON data via an HTTP POST.

Unlike the Danlaw brokers, the content of an incoming JSON message does not have to conform to a
predefined data model when sent via HTTP. As long as the message is valid JSON, the HTTP broker
will create an event containing the payload data, and what was sent will be passed through unmodified.

## Messages

The only required field in an HTTP message is `deviceId`. 

There are two ways to provide the device ID. The first method
identifies a device in the JSON payload. The second method identifies a device
using a device header. Both methods result in the same event data production.

### Device ID in the Request Body

Device authentication and authorization use the `deviceId` field of the request
object. Event data is generated from the contents of the `payload` field.

`POST  http://mesos-slave-pen-lb-us-east-1-production.hub.bitbrew.com:9003/v1/event`

#### Request Body

##### Attributes

- deviceId: `6020981915` (required, string) - The device identifier to associate with this message
- payload: (object) - An object that contains the event data. Can contain any arbitrarily nested objects and properties.

##### Example

```json
{
    "deviceId": "6020981915",
    "payload": {
      "foo": "bar",
      "qux": {
        "baz": [1, 2, 3]
      }
    }
}
```

#### Example Event

```json
{
  "foo": "bar",
  "qux": {
    "baz": [1, 2, 3]
  }
}
```

### Device ID in the Header

Device authentication and authorization use the `X-Device-Id` header value of
the request. Event data is generated from the JSON object in the request body.

`POST http://mesos-slave-pen-lb-us-east-1-production.hub.bitbrew.com:9003/v2/event`

#### Headers
| Key           | Value            |
| ------------- | ---------------- |
| X-Device-Id   | {deviceId}       |

#### Request Body

```json
{
  "foo": "bar",
  "qux": {
    "baz": [1, 2, 3]
  }
}
```

#### Example Event

```json
{
  "foo": "bar",
  "qux": {
    "baz": [1, 2, 3]
  }
}
```

### Broker Type Name

When creating an HTTP device broker for a device on the platform, the string to input is `Http`.
```
{
   "type": "Http"
}
```
