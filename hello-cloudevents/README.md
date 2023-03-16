# Hello CloudEvents

 A minimal CloudEvents triggered service.

Start the server:

```sh
dotnet run
```

Inside the [scripts](scripts) folder:

```sh
./send_cloudevent_binary_http.sh

Send a CloudEvent in binary-mode over HTTP
Attributes are sent as ce- headers and data is encoded in the message body

curl localhost:8080 -v \
  -X POST \
  -H "Content-Type: application/json" \
  -H "ce-specversion: 1.0" \
  -H "ce-type: com.mycompany.myapp.myservice.myevent" \
  -H "ce-source: myservice/mysource" \
  -H "ce-id: 1234-5678" \
  -H "ce-time: 2023-01-02T12:34:56.789Z" \
  -H "ce-subject: my-important-subject" \
  -d '{
        "foo1": "bar1",
        "foo2": "bar2"
      }'
```

```sh
./send_cloudevent_structured_http.sh

Send a CloudEvent in structured-mode over HTTP
Entire event (attribues and data) are encoded in the message body

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
        "data": {
          "foo1": "bar1",
          "foo2": "bar2"
        }
      }'
```

The server receives both events:

```log
info: Microsoft.AspNetCore.Routing.EndpointMiddleware[0]
      Executing endpoint '/ HTTP: POST'
CloudEvent information:
  ID: 1234-5678
  Source: myservice/mysource
  Type: com.mycompany.myapp.myservice.myevent
  Subject: my-important-subject
  DataSchema:
  DataContentType: application/json
  Time: 2023-01-02T12:34:56.789Z
  SpecVersion: 1.0
```
