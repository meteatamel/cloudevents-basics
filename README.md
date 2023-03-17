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

### CloudEvent Format

### TODO

* CloudEvents Attributes and custom attributes
* Content Modes: Binary, Structured, Batched
* Protocol Bindings: AMQP, HTTP, Kafka, MQTT, NATS, WebSockets
* Event Formats: AVRO, JSON, Protobuf, XML
* SDKs: Go, Javascript, Java, C#, Ruby, PHP, Python, Rust, Powershell
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
