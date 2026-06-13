JavaScript SDK
==============

The Nexacon JavaScript SDK provides a comprehensive solution for integrating the Nexacon API into JavaScript and TypeScript applications for both browser and Node.js environments.

.. toctree::
   :maxdepth: 2
   :caption: JavaScript SDK:

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

The JavaScript SDK offers:

* **Browser support** - Modern browsers with ES6+ support
* **Node.js support** - Server-side applications
* **TypeScript support** - Full type definitions included
* **Real-time messaging** - Message streams, typing indicators, read receipts
* **Audio/Video calling** - WebRTC-based P2P and group calls
* **Device management** - Push notification registration
* **Presence** - User online status and last seen

Installation
------------

.. code-block:: bash

    npm install nexacon-sdk
    # or
    yarn add nexacon-sdk
    # or
    pnpm add nexacon-sdk

See `Installation Guide <installation.html>`_ for detailed setup instructions.

Quick Start
-----------

.. code-block:: typescript

    import { NexaconClient } from 'nexacon-sdk';

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

| Platform | Status | Notes |
|----------|--------|-------|
| Browser | ✅ Stable | Chrome, Firefox, Safari, Edge |
| Node.js | ✅ Stable | Version 14.0.0+ |

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

See the `JavaScript SDK examples <https://github.com/nexacon/nexacon-js-sdk/tree/main/examples>`_ for complete sample applications.

Support
-------

* **Documentation**: https://docs.nexacon.com
* **GitHub**: https://github.com/nexacon/nexacon-js-sdk
* **Issues**: https://github.com/nexacon/nexacon-js-sdk/issues
