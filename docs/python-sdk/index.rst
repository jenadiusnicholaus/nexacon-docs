Python SDK
==========

The Nexacon Python SDK provides a comprehensive solution for integrating the Nexacon API into Python applications for server-side and desktop use.

.. toctree::
   :maxdepth: 2
   :caption: Python SDK:

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

The Python SDK offers:

* **Python 3.7+ support** - Modern Python versions
* **Type hints** - Full type annotations
* **Async support** - Async/await for asynchronous operations
* **Real-time messaging** - Message streams, typing indicators, read receipts
* **Audio/Video calling** - WebRTC-based P2P and group calls
* **Device management** - Push notification registration
* **Presence** - User online status and last seen

Installation
------------

.. code-block:: bash

    pip install nexacon-sdk

See `Installation Guide <installation.html>`_ for detailed setup instructions.

Quick Start
-----------

.. code-block:: python

    from nexacon_sdk import NexaconClient

    # Initialize client
    client = NexaconClient(
        api_key='your_api_key',
        secret_key='your_secret_key'
    )

    # Authenticate user
    token = client.auth.login(
        username='user@example.com',
        password='password'
    )

    # Send message
    client.messaging.send(
        to='+255788811191',
        message='Hello!'
    )

Platform Support
----------------

.. list-table:: Platform Support
   :widths: 25 15 60
   :header-rows: 1

   * - Platform
     - Status
     - Notes
   * - Linux
     - ✅ Stable
     - Full support
   * - macOS
     - ✅ Stable
     - Full support
   * - Windows
     - ✅ Stable
     - Full support

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
* **GitHub**: https://github.com/nexacon/nexacon-python-sdk
* **Issues**: https://github.com/nexacon/nexacon-python-sdk/issues
