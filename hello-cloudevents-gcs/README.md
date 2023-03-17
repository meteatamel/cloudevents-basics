# Hello CloudEvents - GCS

 A Google Cloud Storage CloudEvents triggered service.

Start the server:

```sh
dotnet run
```

Inside the [scripts](scripts) folder:

```sh
./send_cloudevent_binary_http.sh

Send binary-mode CloudEvent over HTTP
Attributes are sent as ce- headers and data is encoded in the message body

curl localhost:8080 -v \
  -X POST \
  -H "Content-Type: application/json" \
  -H "ce-id: 123451234512345" \
  -H "ce-specversion: 1.0" \
  -H "ce-time: 2020-01-02T12:34:56.789Z" \
  -H "ce-type: google.cloud.storage.object.v1.finalized" \
  -H "ce-source: //storage.googleapis.com/projects/_/buckets/MY-BUCKET-NAME" \
  -H "ce-subject: objects/MY_FILE.txt" \
  -d '{
        "bucket": "MY_BUCKET",
        "contentType": "text/plain",
        "kind": "storage#object",
        "md5Hash": "...",
        "metageneration": "1",
        "name": "MY_FILE.txt",
        "size": "352",
        "storageClass": "MULTI_REGIONAL",
        "timeCreated": "2020-04-23T07:38:57.230Z",
        "timeStorageClassUpdated": "2020-04-23T07:38:57.230Z",
        "updated": "2020-04-23T07:38:57.230Z"
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
        "type": "google.cloud.storage.object.v1.finalized",
        "source": "//storage.googleapis.com/projects/_/buckets/MY-BUCKET-NAME",
        "id": "1234-5678",
        "time": "2023-01-02T12:34:56.789Z",
        "subject": "objects/MY_FILE.txt",
        "datacontenttype": "application/json",
        "data": {
          "bucket": "MY_BUCKET",
          "contentType": "text/plain",
          "kind": "storage#object",
          "md5Hash": "...",
          "metageneration": "1",
          "name": "MY_FILE.txt",
          "size": "352",
          "storageClass": "MULTI_REGIONAL",
          "timeCreated": "2020-04-23T07:38:57.230Z",
          "timeStorageClassUpdated": "2020-04-23T07:38:57.230Z",
          "updated": "2020-04-23T07:38:57.230Z"
        }
      }'
```

The server receives both events:

```log
info: Microsoft.AspNetCore.Routing.EndpointMiddleware[0]
      Executing endpoint '/ HTTP: POST'
CloudEvent information:
  ID: 1234-5678
  Source: //storage.googleapis.com/projects/_/buckets/MY-BUCKET-NAME
  Type: google.cloud.storage.object.v1.finalized
  Subject: objects/MY_FILE.txt
  DataSchema: 
  DataContentType: application/json
  Time: 2023-01-02T12:34:56.789Z
  SpecVersion: 1.0
Storage object information:
  Name: MY_FILE.txt
  Bucket: MY_BUCKET
  Size: 352
  Content type: text/plain
```
