Flutter SDK Quick Start
=======================

Get up and running with the Nexacon Flutter SDK in minutes.

Initialize the Client
---------------------

.. code-block:: dart

    import 'package:nexacon_sdk/nexacon_sdk.dart';

    final client = NexaconClient(
      apiKey: 'your_api_key',
      secretKey: 'your_secret_key',
    );

Available Services
------------------

Once the client is initialized, all services are available:

.. code-block:: dart

    client.auth        // Authentication and token management
    client.calls       // Audio/video calls
    client.messaging   // Send messages and manage contacts
    client.devices     // Device registration for push notifications
    client.rooms       // Group chat rooms
    client.presence    // User presence and online status

Authentication
--------------

.. code-block:: dart

    // Set the NX token (obtained from Nexacon dashboard)
    client.setToken('your_nx_token');

    // Generate XMPP token for real-time features
    final nxResponse = await client.auth.generateXMPPToken(
      username: '+255788811191',
    );

    print('XMPP token: ${nxResponse['token']}');
    print('JID: ${nxResponse['jid']}');
    print('WebSocket URL: ${nxResponse['nxws']}');

Messaging
---------

.. code-block:: dart

    // Create messaging manager
    final messagingManager = client.createMessagingManager();

    // Listen for incoming messages
    messagingManager.messageStream.listen((message) {
      print('Received: ${message['message']}');
    });

    // Send a message
    await messagingManager.sendMessage(
      to: '+255788811191',
      message: 'Hello!',
    );

    // Get message history
    final messages = await messagingManager.getHistory(
      recipient: '+255788811191',
      page: 1,
      pageSize: 50,
    );

Calls
-----

.. code-block:: dart

    // Generate NX token
    final nxResponse = await client.auth.generateXMPPToken(
      username: '+255788811191',
    );

    // Create CallManager
    final callManager = await client.createCallManager(
      nxtoken: nxResponse['token'],
      nxid: nxResponse['jid'],
      wsUrl: nxResponse['nxws'],
      onCallStateChanged: (state) => print('State: $state'),
      onIncomingCall: (caller) => print('Incoming from: $caller'),
    );

    // Make a call
    await callManager.initiateCall(
      to: '+255788811191',
      callType: 'video',
    );

    // End a call
    await callManager.endCall();

Device Registration
-------------------

.. code-block:: dart

    // Register device for push notifications
    await client.devices.register(
      fcmToken: 'device_fcm_token',
      platform: 'android',
    );

Presence
--------

.. code-block:: dart

    // Get user presence
    final presence = await client.presence.getStatus('+255788811191');
    print('Online: ${presence['online']}');

    // Get last seen
    final lastSeen = await client.presence.getLastSeen('+255788811191');
    print('Last seen: ${lastSeen['timestamp']}');

Foldable Device Support
-----------------------

.. code-block:: dart

    // Get current fold state
    final foldState = client.foldStateService.currentState;
    print('Fold state: $foldState');

    // Listen for fold state changes
    client.foldStateService.foldStateStream.listen((state) {
      print('Fold state changed: $state');
    });

Complete Example
----------------

.. code-block:: dart

    import 'package:nexacon_sdk/nexacon_sdk.dart';

    void main() async {
      // Initialize client
      final client = NexaconClient(
        apiKey: 'your_api_key',
        secretKey: 'your_secret_key',
      );

      // Set NX token (obtained from Nexacon dashboard)
      client.setToken('your_nx_token');

      // Generate XMPP token for real-time features
      final nxResponse = await client.auth.generateXMPPToken(
        username: '+255788811191',
      );

      // Send message
      final messagingManager = client.createMessagingManager();
      await messagingManager.sendMessage(
        to: '+255788811191',
        message: 'Hello from Flutter!',
      );

      // Make a call
      final callManager = await client.createCallManager(
        nxtoken: nxResponse['token'],
        nxid: nxResponse['jid'],
        wsUrl: nxResponse['nxws'],
      );

      await callManager.initiateCall(
        to: '+255788811191',
        callType: 'video',
      );
    }

Next Steps
----------

* `API Reference <api-reference.html>`_ - Detailed API documentation
* `Messaging <messaging.html>`_ - Messaging features
* `Calls <calls.html>`_ - Calling features
* `Best Practices <../guides/best-practices.html>`_ - Recommended practices
