# CloudEvents Basics

![CloudEvents Logo](https://avatars.githubusercontent.com/u/32076828?s=200&v=4)

This repository contains information, references, and samples about CloudEvents.

## Topics

### CloudEvents: Why? What?

CloudEvents is a specification for describing event data in a common way with
the goal of increasing interoperability between different event systems.

CloudEvents, at its core, defines a set of metadata, called "context
attributes". This metadata is the minimal set of information needed to route the
request to the proper component. Data that is not intended for routing is placed
within the `data` (or base64 encoded `data_base64`) field of CloudEvent.

### What does a CloudEvent look like?

Binary-mode:

```sh
curl localhost:8080 -v \
  -X POST \
  -H "Content-Type: application/json" \
  -H "ce-specversion: 1.0" \
  -H "ce-type: com.mycompany.myapp.myservice.myevent" \
  -H "ce-source: myservice/mysource" \
  -H "ce-id: 1234-5678" \
  -H "ce-time: 2023-01-02T12:34:56.789Z" \
  -H "ce-subject: my-important-subject" \
  -H "ce-extensionattr1: value" \
  -H "ce-extensionattr2: 5" \
  -d '{
        "foo1": "bar1",
        "foo2": "bar2"
      }'
```

Structured-mode:

```sh
curl localhost:8080 -v \
  -X POST \
  -H "Content-Type: application/cloudevents+json" \
  -d '{
        "specversion": "1.0",
        "type": "com.mycompany.myapp.myservice.myevent",
        "source": "myservice/mysource",
        "id": "1234-5678",
        "time": "2023-01-02T12:34:56.789Z",
        "subject": "my-important-subject",
        "datacontenttype": "application/json",
        "extensionattr1" : "value",
        "extensionattr2" : 5,
        "data": {
          "foo1": "bar1",
          "foo2": "bar2"
        }
      }'
```

### CloudEvent Attributes

**Core** attributes are defined by spec and divided into required and optional:

Required:

* specversion
* id
* source
* type

Optional:

* subject
* time
* datacontenttype
* dataschema

**Extension** attributes ae additional metadata to help proper routing and
processing of the CloudEvent.

### Content Modes

There are 3 content modes in CloudEvents: binary, structured, batched.

* **Binary-mode**: The event data is stored in the message body, and event
  attributes are stored as part of message metadata. Allows for efficient
  transfer and without transcoding effort. Good for supporting receivers that
  might not be aware of CloudEvents as the metadata can be ignored.
* **Structured-mode**: Keeps event metadata and data together in the payload,
  allowing simple forwarding of the same event across multiple routing hops, and
  across multiple protocols.
* **Batch-mode**: Multiple (zero or more) events are encoded in a single message
  body, according to a specific event format.

**Batch-mode is not supported in all protocol/SDK combinations**. For example,
Javascript SDK supports HTTP and Kafka batch mode but not MQTT batch mode.

### Event Formats

Defines how the CloudEvent is serialized:

* JSON
* Protobuf
* Avro
* XML (draft)

**Not all event formats are supported in each SDK. JSON is the most supported one.**

### Protocol Bindings

Defines how the CloudEvent is bound to an application protocol's transport frame:

* HTTP
* AMQP
* Kafka
* MQTT
* NATS
* WebSockets (draft)

**Not all protocol bindings are supported in each SDK. HTTP is the most
supported one.** For example, Javascript SDK supports HTTP and Kafka but not
AMQP, MQTT, NATS

### SDKs

There are [CloudEvents SDKs](https://github.com/cloudevents/) to read and write
CloudEvents in various languages: Go, Javascript, Java, C#, Ruby, PHP, Python,
Rust, Powershell.

### Google CloudEvents and libraries

This repository contains types for CloudEvents issued by Google:

* [googleapis/google-cloudevents](https://github.com/googleapis/google-cloudevents)

Google CloudEvent Type Libraries help you to parse the `data` field of
CloudEvents:

* [Node.js](https://github.com/googleapis/google-cloudevents-nodejs)
* [Python](https://github.com/googleapis/google-cloudevents-python)
* [Go](https://github.com/googleapis/google-cloudevents-go)
* [Java](https://github.com/googleapis/google-cloudevents-java)
* *[.NET](https://github.com/googleapis/google-cloudevents-dotnet)

### New specs

These are works-in-progress specs:

* Discovery API
* Subscriptions API
* Schema Registry

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
