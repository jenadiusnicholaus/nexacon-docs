Go SDK
======

The Nexacon Go SDK provides a comprehensive solution for integrating the Nexacon API into Go applications for server-side and microservices use.

.. toctree::
   :maxdepth: 2
   :caption: Go SDK:

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

The Go SDK offers:

* **Go 1.16+ support** - Modern Go versions
* **Concurrent operations** - Built-in goroutine support
* **Type-safe** - Strong typing with Go
* **Real-time messaging** - Message streams, typing indicators, read receipts
* **Audio/Video calling** - WebRTC-based P2P and group calls
* **Device management** - Push notification registration
* **Presence** - User online status and last seen

Installation
------------

.. code-block:: bash

    go get github.com/nexacon/nexacon-go-sdk

See `Installation Guide <installation.html>`_ for detailed setup instructions.

Quick Start
-----------

.. code-block:: go

    package main

    import "github.com/nexacon/nexacon-go-sdk"

    func main() {
        // Initialize client
        client := nexacon.NewClient("your_api_key", "your_secret_key")

        // Authenticate user
        token, _ := client.Auth.Login("user@example.com", "password")

        // Send message
        client.Messaging.Send("+255788811191", "Hello!")
    }

Platform Support
----------------

| Platform | Status | Notes |
|----------|--------|-------|
| Linux | ✅ Stable | Full support |
| macOS | ✅ Stable | Full support |
| Windows | ✅ Stable | Full support |

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
* **GitHub**: https://github.com/nexacon/nexacon-go-sdk
* **Issues**: https://github.com/nexacon/nexacon-go-sdk/issues
