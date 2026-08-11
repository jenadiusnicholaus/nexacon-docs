Calls
=====

The calling service provides audio and video calling capabilities using WebRTC for peer-to-peer and group calls.

For detailed API reference, see `API Reference <api-reference.html#nexaconsdk>`_.

Features
--------

* **P2P Calls** - One-to-one audio and video calls
* **Group Calls** - Multi-participant calls
* **WebRTC** - Real-time communication
* **Call Controls** - Mute, speaker, camera switch, video toggle
* **Call Duration** - Track call duration
* **Pre-warming** - Establish connection before call for faster setup
* **Push Notification Accept** - Accept calls from FCM data without waiting for signaling

Quick Example
-------------

.. code-block:: dart

    final sdk = NexaconSDK(
      apiKey: 'your_api_key',
      secretKey: 'your_secret_key',
    );

    // Set callbacks
    sdk.onCallStateChanged = (state) => print('State: $state');
    sdk.onIncomingCall = (caller) => print('Incoming from: $caller');
    sdk.onCallEnded = (reason) => print('Call ended: $reason');
    sdk.onLocalStream = () => print('Local stream ready');
    sdk.onRemoteStream = () => print('Remote stream ready');

    // Make a call
    await sdk.startCall(
      to: '+255788811191',
      username: '+255123456789',
      audio: true,
      video: false,
    );

    // Call controls
    sdk.toggleMute(true);     // Mute
    sdk.toggleSpeaker(true);  // Speaker on
    sdk.toggleVideo(true);    // Camera on
    await sdk.switchCamera(); // Switch camera

    // End the call
    await sdk.endCall();
    await sdk.dispose();

See `Quick Start <quickstart.html>`_ for more examples.
