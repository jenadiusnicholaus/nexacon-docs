React Native SDK
================

The Nexacon React Native SDK provides a comprehensive solution for integrating the Nexacon API into React Native applications for iOS and Android platforms.

.. toctree::
   :maxdepth: 2
   :caption: React Native SDK:

   installation
   quickstart
   api-reference
   messaging
   calls
   devices
   rooms
   presence

Overview
--------

The React Native SDK offers:

* **iOS support** - Native iOS integration
* **Android support** - Native Android integration
* **TypeScript support** - Full type definitions included
* **Real-time messaging** - Message streams, typing indicators, read receipts
* **Audio/Video calling** - WebRTC-based P2P and group calls
* **Device management** - Push notification registration
* **Presence** - User online status and last seen

Installation
------------

.. code-block:: bash

    npm install nexacon-react-native-sdk
    # or
    yarn add nexacon-react-native-sdk

See `Installation Guide <installation.html>`_ for detailed setup instructions.

Quick Start
-----------

.. code-block:: typescript

    import { NexaconClient } from 'nexacon-react-native-sdk';

    // Initialize client
    const client = new NexaconClient({
      apiKey: 'your_api_key',
      secretKey: 'your_secret_key',
    });

    // Authenticate user
    const token = await client.auth.login({
      username: 'user@example.com',
      password: 'password',
    });

    // Send message
    await client.messaging.send({
      to: '+255788811191',
      message: 'Hello!',
    });

    // Initiate call
    const call = await client.calls.initiateCall({
      to: '+255788811191',
      callType: 'video',
      room: 'my-room',
    });

Platform Support
----------------

.. list-table:: Platform Support
   :widths: 25 15 60
   :header-rows: 1

   * - Platform
     - Status
     - Notes
   * - iOS
     - ✅ Stable
     - iOS 12.0+
   * - Android
     - ✅ Stable
     - Android 5.0+ (API 21+)

Features
--------

**Authentication**

* User login with username/password
* Token management and refresh
* Session handling

**Messaging**

* Send and receive messages
* Message history with filters
* Typing indicators
* Read receipts
* Delivery receipts
* Presence management

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

* Create and manage group chat rooms
* Room member management
* Room messages

**Presence**

* User online status
* Last seen information
* Presence streams

API Reference
------------

See `API Reference <api-reference.html>`_ for detailed API documentation.

Examples
--------

See the `React Native SDK examples <https://github.com/nexacon/nexacon-react-native-sdk/tree/main/examples>`_ for complete sample applications.

Support
-------

* **Documentation**: https://docs.nexacon.com
* **GitHub**: https://github.com/nexacon/nexacon-react-native-sdk
* **Issues**: https://github.com/nexacon/nexacon-react-native-sdk/issues
