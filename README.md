# JMF-Subscription
If you want to get some information from your Indigo/DFE, you can always send it a JMF. But if you are actively monitoring the status of the device, you're better off with a JMF subscription which will notify an HTTP endpoint when something changes. Below you'll find an example on how to implement a basic JMF subscription endpoint using Node.

## subscribe.js
Use this script to search and subscribe to your JMF devices. Takes two arguments. '--idp' is the URL to your IDP worker (on your DFE) and should end with /jmf/. '--server' is the IP and port of your JMF server (see server.js).

```
dominick$ node subscribe.js --idp http://192.168.1.40:8080/dpp/jmf/ --server http://192.168.1.70:9090
info: Found Device ID: 192.168.1.45
info: Found Device ID: HP-Indigo-BUDPB
info: 2 two presses found.
info:  http=http://192.168.1.40:8080/dpp/jmf/192.168.1.45
info:  http=http://192.168.1.40:8080/dpp/jmf/HP-Indigo-BUDPB
info:  result=HP-Indigo-BUDPB subscribed successfully.
info:  result=192.168.1.45 subscribed successfully.
```

## server.js
This simple server opens a port and listens for subscription events from the JMF devices. Takes one argument. '--port' is the port the server should listen on.

```
dominick$ node server.js --port 9090
Server listening on: http://localhost:9090
info:  DeviceID=HP-Indigo-BUDPB, DeviceStatus=Running, StatusDetails=Indigo: Printing, ProductionCounter=49942091
info:  DeviceID=HP-Indigo-BUDPB, DeviceStatus=Running, StatusDetails=Indigo: Printing, ProductionCounter=49942098
info:  DeviceID=HP-Indigo-BUDPB, DeviceStatus=Running, StatusDetails=Indigo: Printing, ProductionCounter=49942109
info:  DeviceID=HP-Indigo-BUDPB, DeviceStatus=Idle, StatusDetails=Indigo: Ready, ProductionCounter=49942109
info:  DeviceID=192.168.1.45, DeviceStatus=Idle, StatusDetails=Indigo: Ready, ProductionCounter=35089299
info:  DeviceID=192.168.1.45, DeviceStatus=Running, StatusDetails=Indigo: Printing, ProductionCounter=35089299

```

The server also saves the JMF details in a simple nebd database.

## Info
For more information, see this post for now: http://forum.enfocus.com/viewtopic.php?f=13&t=761

## Todo
- Cancel subscriptions
- Different type of subscriptions (QueueStatus)
