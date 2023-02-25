# Comunicação / Mensagens

## Eventos

`IEventManager`

`IEventHandler`

### Pub/Sub

`IEventPublisher`

`IEventSubscriber`

### Send/Receive

### Request/Response

<br>
<br>

## Notification Pattern

`INotificationHandler`

<br>
<br>

## EasyNetQ

### **Publish / Subscribe**

Publish

```C#
var message = new MyMessage { Text = "Hello Rabbit" };
await bus.PubSub.PublishAsync(message).ConfigureAwait(false);
```

Subscribe

```C#
bus.PubSub.Subscribe<MyMessage>("my_subscription_id", msg => Console.WriteLine(msg.Text));
```

### **Request / Response**

Request

```C#
var myRequest = new MyRequest { Text = “Hello Server” };
var response = bus.Rpc.Request<MyRequest, MyResponse>(myRequest);
Console.WriteLine(response.Text);
```

Asynchronous request

```C#
var task = bus.Rpc.RequestAsync<TestRequestMessage, TestResponseMessage>(request)
task.ContinueWith(response => {
    Console.WriteLine("Got response: '{0}'", response.Result.Text);
});
```

Responding to requests

```C#
bus.Rpc.Respond<MyRequest, MyResponse>(request => new MyResponse { Text = "Responding to" + request.Text});
```

### **Send / Receive**

Send

```C#
bus.SendReceive.Send("my.queue", new MyMessage{ Text = "Hello Widgets!" });
```

Receive

```C#
bus.SendReceive.Receive("my.queue", x => x
    .Add<MyMessage>(message => deliveredMyMessage = message)
    .Add<MyOtherMessage>(message => deliveredMyOtherMessage = message));
```
