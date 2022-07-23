## Start MQTT Client with C#

we're going to have a look at What is MQTT and how can create a simple MQTT client.

But first, we need to know ...
## What is MQTT?
according to MQTT.org:

`MQTT is an OASIS standard messaging protocol for the Internet of Things (IoT). It is designed as an extremely lightweight publish/subscribe messaging transport that is ideal for connecting remote devices with a small code footprint and minimal network bandwidth. MQTT today is used in a wide variety of industries, such as automotive, manufacturing, telecommunications, oil and gas, etc.`

### MQTT Publish / Subscribe Architecture 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1641992891720/E49yUI_TW.png)


### Broker
 ** The broker is responsible for receiving all messages, filtering the messages, determining who is subscribed to each message, and sending the message to these subscribed clients. ** The broker is at the heart of any publish/subscribe protocol. Depending on the implementation, a broker can handle up to millions of concurrently connected MQTT clients.

### Client
** An MQTT client is any device (from a microcontroller up to a full-fledged server) that runs an MQTT library and connects to an MQTT broker over a network. **

## Code a simple client

### Create a project

We need to create a console project I use dotnet CLI to create a new project
```
dotnet new console --name SimpleMQTTClient
```
Now We have a new empty project 😁.
### Install dependency 
For working in dotnet with MQTT we need to install the  [MQTTnet.Extensions.ManagedClient](https://www.nuget.org/packages/MQTTnet.Extensions.ManagedClient) package from NuGet. 
```
dotnet add package MQTTnet.Extensions.ManagedClient --version 3.1.1
```
At this time last stable version of `MQTTnet` is `3.1.1`.

### Implemention 
Now it's time to have some fun in code. Open `Program.cs` 
```
using MQTTnet;
using MQTTnet.Client.Connecting;
using MQTTnet.Client.Disconnecting;
using MQTTnet.Client.Options;
using MQTTnet.Extensions.ManagedClient;
using System.Text.Json;


// Create the client object
IManagedMqttClient _mqttClient = new MqttFactory().CreateManagedMqttClient();

// Create client options object
MqttClientOptionsBuilder builder = new MqttClientOptionsBuilder()
                                        .WithClientId("behroozbc")
                                        .WithTcpServer("localhost");
ManagedMqttClientOptions options = new ManagedMqttClientOptionsBuilder()
                        .WithAutoReconnectDelay(TimeSpan.FromSeconds(60))
                        .WithClientOptions(builder.Build())
                        .Build();



// Set up handlers
_mqttClient.ConnectedHandler = new MqttClientConnectedHandlerDelegate((e) => Console.WriteLine("Connected"));
_mqttClient.DisconnectedHandler = new MqttClientDisconnectedHandlerDelegate((e) => Console.WriteLine("Disconnected"));
_mqttClient.ConnectingFailedHandler = new ConnectingFailedHandlerDelegate((e) => Console.WriteLine("Connection failed check network or broker!"));

// Connect to broker
await _mqttClient.StartAsync(options);

// Send a new message to the broker every second
while (true)
{
    string json = JsonSerializer.Serialize(new { message = "Hi Mqtt", sent = DateTime.UtcNow });
    await _mqttClient.PublishAsync("behroozbc.ir/topic/json", json);

    await Task.Delay(TimeSpan.FromSeconds(1));
}
```
By default MQTT without encryption port is 1883 if you want to change it add a parameter port number to `WithTcpServer` like 
```
// Create client options object
MqttClientOptionsBuilder builder = new MqttClientOptionsBuilder()
                                        .WithClientId("behroozbc")
                                        .WithTcpServer("localhost",5004);
```
### Conclusion
You have an MQTT client. I hope it was useful.
In this [post](https://blog.behroozbc.ir/basic-mqtt-broker-with-c-sharp), I will show you how to create a broker to test it.

You find this project on  [Github](https://github.com/behroozbc/SimpleMQTTClient).

If you are still unsure of what to do or if you got any errors,  I suggest you use the comment section below and let me know! I’m here to help.

## Update
A new version of the MQTT library for DotNet was released recently, which introduced many breaking changes, so that you can read the article about it on [this page](https://blog.behroozbc.ir/mqtt-client-with-mqttnet-and-c). 