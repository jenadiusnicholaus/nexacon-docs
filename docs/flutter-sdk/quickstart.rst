Flutter SDK Quick Start
=======================

Get up and running with the Nexacon Flutter SDK in minutes.

Create the SDK Instance
-----------------------

.. code-block:: dart

    import 'package:nexacon_sdk/nexacon_sdk.dart';

    final sdk = NexaconSDK(
      apiKey: 'your_api_key',
      secretKey: 'your_secret_key',
    );

Set Up Callbacks
----------------

.. code-block:: dart

    sdk.onCallStateChanged = (CallState state) {
      print('Call state: $state');
      if (state == CallState.connected) {
        // Call connected — start your UI timer
      }
    };

    sdk.onIncomingCall = (callerName) {
      print('Incoming call from: $callerName');
      // Show incoming call UI
    };

    sdk.onCallEnded = (reason) {
      print('Call ended: $reason');
      // Clean up call UI
    };

    sdk.onError = (error) {
      print('Error: $error');
    };

    sdk.onLocalStream = () {
      // Local media stream is ready — render local preview
    };

    sdk.onRemoteStream = () {
      // Remote media stream is ready — render remote video
    };

    sdk.onOtherUserJoined = () {
      // Remote peer has joined the call
    };

    sdk.onOtherUserLeft = () {
      // Remote peer has left the call
    };

Request Permissions
-------------------

Before making or receiving calls, request microphone and camera permissions:

.. code-block:: dart

    // Using permission_handler package
    final micStatus = await Permission.microphone.request();
    final camStatus = await Permission.camera.request();

    if (!micStatus.isGranted) {
      // Handle denied permission
    }

Make an Outgoing Call
---------------------

.. code-block:: dart

    // startCall() handles everything: fetches NX token, connects, and initiates the call
    await sdk.startCall(
      to: '+255788811191',
      username: '+255123456789',
      name: 'John Doe',
      audio: true,
      video: false,
    );

Pre-warm for Outgoing Calls
---------------------------

For faster call setup, pre-warm the connection before the user taps call:

.. code-block:: dart

    // Call this when the user opens the dialer screen
    await sdk.initialize(
      username: '+255123456789',
      name: 'John Doe',
    );

    // Later, when the user taps call:
    await sdk.startCall(
      to: '+255788811191',
      username: '+255123456789',
    );

Receive an Incoming Call
-----------------------

.. code-block:: dart

    // Pre-warm the connection when the incoming call screen opens
    // This ensures the call invitation is received before the user taps Accept
    await sdk.initialize(
      username: '+255123456789',
      name: 'John Doe',
    );

    // When onIncomingCall fires, accept the call:
    await sdk.acceptCall(audio: true, video: false);

Accept from Push Notification
-----------------------------

When the app is opened from a push notification (FCM), use `acceptFromNotification`_ to bypass waiting for the signaling invitation:

.. code-block:: dart

    await sdk.acceptFromNotification(
      username: '+255123456789',
      roomId: channelName,         // from FCM payload
      callerNxId: callerPhone,     // from FCM payload
      name: 'John Doe',
      audio: true,
      video: false,
    );

Or use `acceptWhenReady`_ to wait for the signaling invitation automatically:

.. code-block:: dart

    await sdk.acceptWhenReady(
      username: '+255123456789',
      name: 'John Doe',
      audio: true,
      video: false,
      timeout: Duration(seconds: 30),
    );

Call Controls
-------------

.. code-block:: dart

    // Mute / unmute microphone
    sdk.toggleMute(true);   // muted
    sdk.toggleMute(false);  // unmuted

    // Toggle speaker
    sdk.toggleSpeaker(true);   // speaker on
    sdk.toggleSpeaker(false);  // speaker off

    // Toggle video
    sdk.toggleVideo(true);   // camera on
    sdk.toggleVideo(false);  // camera off

    // Switch camera (front/back)
    await sdk.switchCamera();

    // Get call duration
    final duration = sdk.callDuration;
    print('Duration: ${duration.inSeconds}s');

End a Call
----------

.. code-block:: dart

    await sdk.endCall();

    // Clean up when done with the SDK
    await sdk.dispose();

Device Registration
-------------------

Access the low-level client for device registration and other services:

.. code-block:: dart

    // Access the underlying NexaconClient for advanced use cases
    final client = sdk.client;

    // Register device for push notifications
    await client?.devices.register(
      fcmToken: 'device_fcm_token',
      platform: 'android',
    );

Presence
--------

.. code-block:: dart

    final client = sdk.client;

    // Get user presence
    final presence = await client?.presence.getStatus('+255788811191');
    print('Online: ${presence?['online']}');

    // Get last seen
    final lastSeen = await client?.presence.getLastSeen('+255788811191');
    print('Last seen: ${lastSeen?['timestamp']}');

Foldable Device Support
-----------------------

.. code-block:: dart

    final client = sdk.client;

    // Get current fold state
    final foldState = client?.foldStateService.currentState;
    print('Fold state: $foldState');

    // Listen for fold state changes
    client?.foldStateService.foldStateStream.listen((state) {
      print('Fold state changed: $state');
    });

Complete Example
----------------

.. code-block:: dart

    import 'package:nexacon_sdk/nexacon_sdk.dart';
    import 'package:permission_handler/permission_handler.dart';

    void main() async {
      // 1. Create SDK instance
      final sdk = NexaconSDK(
        apiKey: 'your_api_key',
        secretKey: 'your_secret_key',
      );

      // 2. Set up callbacks
      sdk.onCallStateChanged = (state) {
        print('Call state: $state');
        if (state == CallState.connected) {
          print('Call connected!');
        }
      };
      sdk.onIncomingCall = (callerName) {
        print('Incoming call from: $callerName');
      };
      sdk.onCallEnded = (reason) {
        print('Call ended: $reason');
      };
      sdk.onLocalStream = () => print('Local stream ready');
      sdk.onRemoteStream = () => print('Remote stream ready');

      // 3. Request permissions
      await Permission.microphone.request();
      await Permission.camera.request();

      // 4. Make a call
      await sdk.startCall(
        to: '+255788811191',
        username: '+255123456789',
        name: 'John Doe',
        audio: true,
        video: false,
      );

      // 5. End the call when done
      await sdk.endCall();
      await sdk.dispose();
    }

.. note::
   For real-time chat messaging (text messages, typing indicators, message history), use the separate `Nexacon Messaging SDK <https://nexacon-messaging.readthedocs.io/>`_.

Next Steps
----------

* `API Reference <api-reference.html>`_ - Detailed API documentation
* `Calls <calls.html>`_ - Calling features
* `Best Practices <../guides/best-practices.html>`_ - Recommended practices
