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
    client.calls       // Audio/video calls (P2P and group)
    client.devices     // Device registration for push notifications
    client.rooms       // Group call rooms
    client.presence    // User presence and online status

Authentication
--------------

.. code-block:: dart

    // Generate NX token for real-time features
    final nxResponse = await client.auth.generateNxToken(
      username: '+255788811191',
    );

    print('NX token: ${nxResponse['token']}');
    print('NX ID: ${nxResponse['nxid']}');
    print('WebSocket URL: ${nxResponse['nxws']}');

Calls
-----

.. code-block:: dart

    // Generate NX token
    final nxResponse = await client.auth.generateNxToken(
      username: '+255788811191',
    );

    // Create CallManager
    final callManager = await client.createCallManager(
      nxtoken: nxResponse['token'],
      nxid: nxResponse['nxid'],
      wsUrl: nxResponse['nxws'],
      onCallStateChanged: (state) => print('State: $state'),
      onIncomingCall: (caller) => print('Incoming from: $caller'),
      onCallEnded: (reason) => print('Call ended: $reason'),
      onLocalStream: (stream) => print('Local stream ready'),
      onRemoteStream: (stream) => print('Remote stream ready'),
    );

    // Make a video call
    await callManager.initiateCall(
      to: '+255788811191',
      video: true,
    );

    // Accept an incoming call
    // await callManager.acceptCall(audio: true, video: true);

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

      // Generate NX token for real-time features
      final nxResponse = await client.auth.generateNxToken(
        username: '+255788811191',
      );

      // Create CallManager with callbacks
      final callManager = await client.createCallManager(
        nxtoken: nxResponse['token'],
        nxid: nxResponse['nxid'],
        wsUrl: nxResponse['nxws'],
        onCallStateChanged: (state) => print('Call state: $state'),
        onIncomingCall: (caller) => print('Incoming call from: $caller'),
        onCallEnded: (reason) => print('Call ended: $reason'),
        onLocalStream: (stream) {
          // Render local video preview
        },
        onRemoteStream: (stream) {
          // Render remote video
        },
      );

      // Make a video call
      await callManager.initiateCall(
        to: '+255788811191',
        video: true,
      );
    }

.. note::
   For real-time chat messaging (text messages, typing indicators, message history), use the separate `Nexacon Messaging SDK <https://nexacon-messaging.readthedocs.io/>`_.

Next Steps
----------

* `API Reference <api-reference.html>`_ - Detailed API documentation
* `Calls <calls.html>`_ - Calling features
* `Best Practices <../guides/best-practices.html>`_ - Recommended practices
