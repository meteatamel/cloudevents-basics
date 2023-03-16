# Node.js - hello-cloudevents

 A minimal CloudEvents triggered Node.js service.

## Start server

Install dependencies:

```sh
npm install
```

Run the function:

```sh
npm start
```

## Test

Inside the [scripts](scripts) folder:

```sh
./send_cloudevent_http_binary.sh

Send binary-mode CloudEvent over HTTP
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
./send_cloudevent_http_structured.sh

Send structured-mode CloudEvent over HTTP
Entire event (attribues and data) are encoded in the message body

curl localhost:8080 -v \
  -X POST \
  -H "Content-Type: application/cloudevents+json" \
  -d '{
        "specversion": "1.0",
        "type": "com.mycompany.myapp.myservice.myevent",
        "source": "myservice/mysource",
        "id: 1234-5678"
        "time": "2023-01-02T12:34:56.789Z",
        "subject": "my-important-subject",
        "data": {
          "foo1": "bar1",
          "foo2": "bar2"
        }
      }'
```
