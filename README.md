# CloudEvents Basics

![CloudEvents Logo](https://avatars.githubusercontent.com/u/32076828?s=200&v=4)

This repository contains information, references, and samples about CloudEvents.

## CloudEvents: Why? What?

[CloudEvents](https://cloudevents.io/) is a specification for describing event
data in a common way with the goal of increasing interoperability between
different event systems.

Google Cloud's [Eventarc](https://cloud.google.com/eventarc/docs), open-source
[Knative](https://knative.dev/docs/), Azure's Event Grid, and many more projects
rely on CloudEvent specification to define their event formats.

CloudEvents, at its core, defines a set of metadata, called "context
attributes". This metadata is the minimal set of information needed to route the
request to the proper component. Data that is not intended for routing is placed
within the `data` (or base64 encoded `data_base64`) field of CloudEvent.

## What does a CloudEvent look like?

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

## CloudEvent Attributes

**Core** attributes are defined by the spec.

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

**Extension** attributes are additional optional metadata to help proper routing
and processing of the CloudEvent. Some [known
extensions](https://github.com/cloudevents/spec/blob/main/cloudevents/documented-extensions.md)
are documented.

## Content Modes

There are 3 content modes in CloudEvents:

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

## Event Formats

Defines how the CloudEvent is serialized:

* JSON
* Protobuf
* Avro
* XML (draft)

**Not all event formats are supported in each SDK. JSON is the most supported
one.** For example, Javascript SDK supports JSON but not Avro or Protobuf.

## Protocol Bindings

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

## SDKs

There are [CloudEvents SDKs](https://github.com/cloudevents/) to read and write
CloudEvents in various languages: 

* [Go](https://github.com/cloudevents/sdk-go)
* [Javascript](https://github.com/cloudevents/sdk-javascript)
* [Java](https://github.com/cloudevents/sdk-java)
* [C#](https://github.com/cloudevents/sdk-csharp)
* [Ruby](https://github.com/cloudevents/sdk-ruby)
* [PHP](https://github.com/cloudevents/sdk-php)
* [Python](https://github.com/cloudevents/sdk-python)
* [Rust](https://github.com/cloudevents/sdk-rust)
* [Powershell](https://github.com/cloudevents/sdk-powershell)

## Google CloudEvents and libraries

This repository contains types for CloudEvents issued by Google:

* [googleapis/google-cloudevents](https://github.com/googleapis/google-cloudevents)

Google CloudEvent Type Libraries help parse the `data` field of
CloudEvents into Google Events:

* [C#](https://github.com/googleapis/google-cloudevents-dotnet)
* [Go](https://github.com/googleapis/google-cloudevents-go)
* [Java](https://github.com/googleapis/google-cloudevents-java)
* [Node.js](https://github.com/googleapis/google-cloudevents-nodejs)
* [Python](https://github.com/googleapis/google-cloudevents-python)

[Eventarc](https://cloud.google.com/eventarc) uses CloudEvents for all of its events.

## Upcoming specs

These are works-in-progress specs:

* Discovery API
* Subscriptions API
* Schema Registry

## Samples

Some samples to show how to read CloudEvents:

* [hello-cloudevents](./hello-cloudevents/) - A minimal CloudEvents triggered
  service using C# CloudEvents SDK.
* [hello-cloudevents-gcs](./hello-cloudevents-gcs/) - A Google Cloud Storage
  CloudEvents triggered service using C# CloudEvents SDK and Google CloudEvent
  Type Library.

## References

Useful links:

* [CloudEvents.io](https://cloudevents.io/)
* [CloudEvents Spec](https://github.com/cloudevents/spec)
* [CloudEvents SDKs](https://github.com/cloudevents/)

Talks:

  * [CloudEvents: Intro, Deep-Dive - Doug Davis, Clemens Vasters, Klaus Deissner & Vladimir Bacvanski](https://youtu.be/yg7RuDWHwV8)
  * [CloudEvents: Intro, Status and the Future - Scott Nichols](https://youtu.be/m1sT-BuA9WU)
  * [CloudEvents And Beyond! - Doug Davis](https://youtu.be/bJTUttZr-Ck)

-------

This is not an official Google product.
