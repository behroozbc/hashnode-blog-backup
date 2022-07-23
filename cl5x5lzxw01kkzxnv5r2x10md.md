## MQTT Client with MQTTnet 4 and C#

In the [previous post](https://blog.behroozbc.ir/start-mqtt-client-with-csharp), we worked with MQTTnet version 3, although version 4 of MQTTnet came in Jun 2022. As MQTTnet version 4 has a lot of changes, I thought it would be helpful to write a new article about developing a simple MQTT broker using this version. To find more information on MQTT and what is MQTT client and broker please check [this post](https://blog.behroozbc.ir/start-mqtt-client-with-csharp).

## Create a project
We need to create a console project. I use dotnet CLI to create a new project.
```
dotnet new console --name SimpleMQTTClient4
```
Now We have a new empty project to code an MQTT client.
## Install Dependency
To work in dotnet with MQTT Client, we need to install the MQTTnet.Extensions.ManagedClient package from NuGet. This article uses version 4.
```
dotnet add package MQTTnet.Extensions.ManagedClient --version 4.0.2.221
```

## Implementation
Open Program.cs.Add the below code.
```
using MQTTnet.Client;
using MQTTnet.Extensions.ManagedClient;
using MQTTnet;
using System.Text.Json;

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
_mqttClient.ConnectedAsync += _mqttClient_ConnectedAsync;


_mqttClient.DisconnectedAsync += _mqttClient_DisconnectedAsync;


_mqttClient.ConnectingFailedAsync += _mqttClient_ConnectingFailedAsync;


// Connect to the broker
await _mqttClient.StartAsync(options);

// Send a new message to the broker every second
while (true)
{
    string json = JsonSerializer.Serialize(new { message = "Hi Mqtt", sent = DateTime.UtcNow });
    await _mqttClient.EnqueueAsync("behroozbc.ir/topic/json", json);

    await Task.Delay(TimeSpan.FromSeconds(1));
}
Task _mqttClient_ConnectedAsync(MqttClientConnectedEventArgs arg)
{
    Console.WriteLine("Connected");
    return Task.CompletedTask;
};
Task _mqttClient_DisconnectedAsync(MqttClientDisconnectedEventArgs arg)
{
    Console.WriteLine("Disconnected");
    return Task.CompletedTask;
};
Task _mqttClient_ConnectingFailedAsync(ConnectingFailedEventArgs arg)
{
    Console.WriteLine("Connection failed check network or broker!");
    return Task.CompletedTask;
}
```
By default MQTT without encryption port is 1883. If you want to change it, add a parameter port number to WithTcpServer.
```
// Create the options for MQTT Broker
var options = new MqttServerOptionsBuilder()
    //Set endpoint to localhost
    .WithDefaultEndpoint()
    // Port is going to use 5004
    .WithDefaultEndpointPort(5004);
```
## Conclusion
You have an MQTT client. I hope it was helpful. In this post, I will show you how to create a broker to test it.

You find this project on [Github](https://github.com/behroozbc/SimpleMQTTClient4).

If you are still unsure of what to do or if you got any errors, I suggest you use the comment section below and let me know! I’m here to help.