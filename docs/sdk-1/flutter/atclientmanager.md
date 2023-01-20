# AtClientManager

#### Overview <a href="#overview" id="overview"></a>

The AtClientManager is in charge of overseeing and managing all client services.It makes NotificationService, SyncService, and Client application preferences easier to access from its instance.It is also used for client method calls.

Based on your need you can either install at\_client\_mobile or at\_client and import. After that you will be able to make an AtClientManager Instance. Now to Initialize the AtClient instance , the setCurrentAtsign method needs to be called.

```
AtClientManager.getInstance().setCurrentAtSign('@alice', 'wavi', <preference>);
```

The setCurrentAtSign method accepts the following arguments: currentAtSign, namespace and the preferences. The currentAtsign argument accepts an atSign , namespace accepts the namespace of the app and the preference accepts AtClientPreference value which we are going to discuss next.

After Initializing you are ready to make calls of client methods and services. The AtClientManager Instance has a getter atClient which returns an instance of AtClient.

#### Usage <a href="#usage" id="usage"></a>

To access CRUD methods :

```
AtClient atClient = atClientManager.atClient;
```

**NotificationService**

Notification service gives back a stream of notifications from the server to the subscribing client.

To access NotificationService methods :

```
NotificationService notificationService = atClientManager.notificationService;
```

**Example**

```
  await atClientManager.notificationService.notify(NotificationParams.forUpdate(<key>,value: <value>));
```

**SyncService**

SyncService syncs the client app and remote secondary server’s changes. If the client app’s changes are ahead, it pushes the changes to the remote secondary. If the remote secondary is ahead, it pulls the changes to the client app.

SyncService which is responsible for invoking the sync :

```
SyncService syncService = atClientManager.syncService;
```
