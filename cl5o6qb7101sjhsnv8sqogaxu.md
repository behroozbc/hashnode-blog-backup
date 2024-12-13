---
title: "C# MQTT broker using MQTTnet version 4"
datePublished: Sat Jul 16 2022 17:50:51 GMT+0000 (Coordinated Universal Time)
cuid: cl5o6qb7101sjhsnv8sqogaxu
slug: c-mqtt-broker-using-mqttnet-version-4
cover: https://cdn.hashnode.com/res/hashnode/image/unsplash/4OhFZSAT3sw/upload/v1657990209534/On50-j1Et.jpeg
tags: csharp, iot, net, internet-of-things

---

In [previous posts](https://blog.behroozbc.ir/basic-mqtt-broker-with-c-sharp), we worked with MQTTnet version 3, although version 4 of MQTTnet came in Jun 2022. As MQTTnet version 4 has a lot of changes, I thought it would be helpful to write a new article about developing a simple MQTT broker using this version.
## What is the MQTT broker?
According to [Wikipedia](https://en.wikipedia.org/wiki/MQTT#:~:text=The%20MQTT%20broker,and%20controlling%20devices.): 

The MQTT broker is software running on a computer (running on-premises or in the cloud) and could be self-built or hosted by a third party. It is available in both open source and proprietary implementations.

The broker acts as a post office; MQTT doesn't use the address of the intended recipient but uses the subject line called "Topic," and anyone who wants a copy of that message will subscribe to that topic. Multiple clients can receive the message from a single broker (one to many capabilities). Similarly, multiple publishers can publish topics to a single subscriber (many to one).

Each client can produce and receive data by publishing and subscribing, i.e., the devices can publish sensor data and still receive the configuration information or control commands (MQTT is a bi-directional communication protocol). This helps in both sharing data and managing and controlling devices.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1642701642862/HwuJmWooB.png)
Now we are on the same page, so we can start coding an MQTT broker.

## Code a simple MQTT broker
### 1) Create a project
We need to create a console project. I use dotnet CLI to create a new project.

```
dotnet new console --name SimpleMQTTBroker4
```
Now we have a new empty project 😁.
### 2) Install dependency
For working in dotnet with MQTT, we need to install the [MQTTnet](https://www.nuget.org/packages/MQTTnet) package from NuGet.
```
dotnet add package MQTTnet --version 4.0.2.221
```
As I mentioned in the introduction, we are using version 4 of this package.

### 3) Implementation
Open `Program.cs`.Add the below code.
```
using MQTTnet.Server;
using MQTTnet;
using System.Text;
using static System.Console;

// Create the options for MQTT Broker
var options = new MqttServerOptionsBuilder()
    //Set endpoint to localhost
    .WithDefaultEndpoint();
// Create a new mqtt server
var server = new MqttFactory().CreateMqttServer(options.Build());
//Add Interceptor for logging incoming messages
server.InterceptingPublishAsync += Server_InterceptingPublishAsync;
// Start the server
await server.StartAsync();
// Keep application running until user press a key
ReadLine();

Task Server_InterceptingPublishAsync(InterceptingPublishEventArgs arg)
{
    // Convert Payload to string
    var payload = arg.ApplicationMessage?.Payload == null ? null : Encoding.UTF8.GetString(arg.ApplicationMessage?.Payload);


    WriteLine(
        " TimeStamp: {0} -- Message: ClientId = {1}, Topic = {2}, Payload = {3}, QoS = {4}, Retain-Flag = {5}",

        DateTime.Now,
        arg.ClientId,
        arg.ApplicationMessage?.Topic,
        payload,
        arg.ApplicationMessage?.QualityOfServiceLevel,
        arg.ApplicationMessage?.Retain);
    return Task.CompletedTask;
}
```
By default, the MQTT without encryption uses port 1883. If you want to change it, use the code below

```
// Create the options for MQTT Broker
var options = new MqttServerOptionsBuilder()
    //Set endpoint to localhost
    .WithDefaultEndpoint()
    // Port going to use 5004
    .WithDefaultEndpointPort(5004);
```
Now you can test the MQTT broker with any MQTT client you own.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1657993569990/oGnd2Gn3V.png align="left")
Note
In this post, We see how we can develop an MQTT broker. I hope it was helpful. You can see the complete code on [Github](https://github.com/behroozbc/SimpleMQTTBroker4).

See other posts on the blog about MQTT and IoT.

If you are still unsure, have questions, or got an error, please feel free to use the comment section below, and I will be happy to assist!