Calls
=====

The calling service provides audio and video calling capabilities using WebRTC for peer-to-peer and group calls.

For detailed API reference, see `API Reference <api-reference.html#callmanager>`_.

Features
--------

* **P2P Calls** - One-to-one audio and video calls
* **Group Calls** - Multi-participant calls
* **WebRTC** - Real-time communication
* **Call Controls** - Mute, speaker, camera switch
* **Call Duration** - Track call duration

Quick Example
-------------

.. code-block:: dart

    final callManager = await client.createCallManager(
      nxtoken: token['token'],
      nxid: token['jid'],
      wsUrl: token['nxws'],
      onCallStateChanged: (state) => print('State: $state'),
      onIncomingCall: (caller) => print('Incoming from: $caller'),
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

    // Accept an incoming call
    // await callManager.acceptCall(audio: true, video: true);

    // Toggle audio/video
    callManager.toggleAudio(false);  // Mute
    callManager.toggleVideo(false);  // Camera off

    // Switch camera
    await callManager.switchCamera();

    // End the call
    await callManager.endCall();

See `Quick Start <quickstart.html>`_ for more examples.
