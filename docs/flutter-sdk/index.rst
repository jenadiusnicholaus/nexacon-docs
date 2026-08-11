Flutter SDK
===========

The Nexacon Flutter SDK provides audio and video calling capabilities for Flutter applications across Android, iOS, Linux, macOS, Web, and Windows platforms.

.. toctree::
   :maxdepth: 2
   :caption: Flutter SDK:

   installation
   quickstart
   api-reference
   calls
   devices
   rooms
   presence
   foldable

Overview
--------

The Flutter SDK offers:

* **Cross-platform support** - Android, iOS, Linux, macOS, Web, Windows
* **Type-safe API** - Full Dart type definitions
* **Audio/Video calling** - WebRTC-based P2P and group calls
* **Device management** - Push notification registration
* **Foldable device support** - Detect fold state on Android
* **Presence** - User online status and last seen

.. note::
   This SDK is for **audio/video calls only**. For real-time chat messaging (text messages, typing indicators, delivery receipts, message history), use the separate `Nexacon Messaging SDK <https://nexacon-messaging.readthedocs.io/>`_.

Installation
------------

.. code-block:: bash

    flutter pub add nexacon_sdk

See `Installation Guide <installation.html>`_ for detailed setup instructions.

Quick Start
-----------

.. code-block:: dart

    import 'package:nexacon_sdk/nexacon_sdk.dart';

    // Initialize client
    final client = NexaconClient(
      apiKey: 'your_api_key',
      secretKey: 'your_secret_key',
    );

    // Authenticate user
    final token = await client.auth.login(
      username: 'user@example.com',
      password: 'password',
    );

    // Initiate call
    final callManager = await client.createCallManager(
      nxtoken: token['token'],
      nxid: token['jid'],
      wsUrl: token['nxws'],
    );

    await callManager.initiateCall(
      to: '+255788811191',
      callType: 'video',
    );

Platform Support
----------------

.. list-table:: Platform Support
   :widths: 25 15 60
   :header-rows: 1

   * - Platform
     - Status
     - Notes
   * - Android
     - ✅ Stable
     - Full support including foldable devices
   * - iOS
     - ✅ Stable
     - Full support
   * - Linux
     - ✅ Stable
     - Desktop support
   * - macOS
     - ✅ Stable
     - Desktop support
   * - Web
     - ✅ Stable
     - Browser support
   * - Windows
     - ✅ Stable
     - Desktop support

Features
--------

**Authentication**

* User login with username/password
* Token management and refresh
* Session handling

**Calls**

* P2P audio/video calls
* Group calls
* WebRTC signaling
* Call controls (mute, speaker, camera)
* Call duration tracking

**Devices**

* Register devices for push notifications
* Platform-specific configuration
* Device management

**Rooms**

* Create and manage group call rooms
* Room member management

**Presence**

* User online status
* Last seen information
* Presence streams

**Foldable Devices**

* Detect fold state (flat, folded, half-open)
* Real-time fold state updates
* Android native integration

Related SDKs
------------

* **Nexacon Messaging SDK** - Real-time chat messaging with presence, typing indicators, delivery receipts, and message history. See `nexacon-messaging docs <https://nexacon-messaging.readthedocs.io/>`_.

API Reference
-------------

See `API Reference <api-reference.html>`_ for detailed API documentation.

Examples
--------

See the `Flutter SDK examples <https://github.com/nexacon/nexacon-flutter-sdk/tree/main/example>`_ for complete sample applications.

Support
-------

* **Documentation**: https://docs.nexacon.africa
* **GitHub**: https://github.com/nexacon/nexacon-flutter-sdk
* **Issues**: https://github.com/nexacon/nexacon-flutter-sdk/issues
