C# SDK
=======

The Nexacon C# SDK provides a comprehensive solution for integrating the Nexacon API into .NET applications for Windows and server-side use.

.. toctree::
   :maxdepth: 2
   :caption: C# SDK:

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

The C# SDK offers:

* **.NET 6.0+ support** - Modern .NET versions
* **NuGet** - Easy dependency management
* **Async/await** - Modern async patterns
* **Real-time messaging** - Message streams, typing indicators, read receipts
* **Audio/Video calling** - WebRTC-based P2P and group calls
* **Device management** - Push notification registration
* **Presence** - User online status and last seen

Installation
------------

.. code-block:: bash

    dotnet add package Nexacon.SDK

See `Installation Guide <installation.html>`_ for detailed setup instructions.

Quick Start
-----------

.. code-block:: csharp

    using Nexacon.SDK;

    // Initialize client
    var client = new NexaconClient("your_api_key", "your_secret_key");

    // Authenticate user
    var token = await client.Auth.LoginAsync("user@example.com", "password");

    // Send message
    await client.Messaging.SendAsync("+255788811191", "Hello!");

Platform Support
----------------

| Platform | Status | Notes |
|----------|--------|-------|
| Windows | ✅ Stable | Full support |
| Linux | ✅ Stable | Full support |
| macOS | ✅ Stable | Full support |

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

Support
-------

* **Documentation**: https://docs.nexacon.com
* **GitHub**: https://github.com/nexacon/nexacon-csharp-sdk
* **Issues**: https://github.com/nexacon/nexacon-csharp-sdk/issues
