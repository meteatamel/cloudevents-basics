# CloudEvents Samples

![CloudEvents Logo](https://avatars.githubusercontent.com/u/32076828?s=200&v=4)

This repository contains information, references, and samples about CloudEvents.

## Topics

### CloudEvents: Why? What?

CloudEvents is a specification for describing event data in a common way with
the goal of increasing interoperability between different event systems.

CloudEvents, at its core, defines a set of metadata, called "context
attributes". This metadata is the minimal set of information needed to route the
request to the proper component. Data that is not intended for routing is placed
within the data field of CloudEvent.

### Content Modes

There are 3 content modes in CloudEvents: binary, structured, batched (in some
cases):

* **Binary-mode**: The event data is stored in the message body, and event
  attributes are stored as part of message metadata. Good for supporting
  receivers that might not be aware of CloudEvents as the metadata can be
  ignored.
* **Structured-mode**: The entire event (attributes and data) are encoded in the
  message body.
* **Batch-moe**: Multiple (zero or more) events are encoded in a single message body, according to a specific event format. Not all event formats or protocol bindings support batch-mode messages


### SDKs

There are [CloudEvents SDKs](https://github.com/cloudevents/) to read and write
CloudEvents in various languages: Go, Javascript, Java, C#, Ruby, PHP, Python,
Rust, Powershell.

### TODO

* CloudEvents Attributes and custom attributes
* Protocol Bindings: AMQP, HTTP, Kafka, MQTT, NATS, WebSockets
* Event Formats: AVRO, JSON, Protobuf, XML
* Google Events libraries
* Next: Discovery API, Subscriptions API, Schema Registry

## Samples

* [hello-cloudevents](./hello-cloudevents/) - A minimal CloudEvents triggered
  service.
* [hello-cloudevents-gcs](./hello-cloudevents-gcs/) - A Google Cloud Storage
  CloudEvents triggered service.

## References

* [CloudEvents.io](https://cloudevents.io/)
* [CloudEvents Spec](https://github.com/cloudevents/spec)
* [CloudEvents SDKs](https://github.com/cloudevents/)
* Talks
  * [CloudEvents: Intro, Status and the Future - Scott Nichols](https://youtu.be/m1sT-BuA9WU)
  * [CloudEvents And Beyond! - Doug Davis](https://youtu.be/bJTUttZr-Ck)

-------

This is not an official Google product.
