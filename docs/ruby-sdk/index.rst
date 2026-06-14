Ruby SDK
=========

The Nexacon Ruby SDK provides a comprehensive solution for integrating the Nexacon API into Ruby applications for web use.

.. toctree::
   :maxdepth: 2
   :caption: Ruby SDK:

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

The Ruby SDK offers:

* **Ruby 2.7+ support** - Modern Ruby versions
* **Bundler** - Easy dependency management
* **Type-safe** - Strong typing with Sorbet
* **Real-time messaging** - Message streams, typing indicators, read receipts
* **Audio/Video calling** - WebRTC-based P2P and group calls
* **Device management** - Push notification registration
* **Presence** - User online status and last seen

Installation
------------

Add to your `Gemfile`:

.. code-block:: ruby

    gem 'nexacon-sdk'

Then run:

.. code-block:: bash

    bundle install

See `Installation Guide <installation.html>`_ for detailed setup instructions.

Quick Start
-----------

.. code-block:: ruby

    require 'nexacon-sdk'

    # Initialize client
    client = NexaconClient.new('your_api_key', 'your_secret_key')

    # Authenticate user
    token = client.auth.login('user@example.com', 'password')

    # Send message
    client.messaging.send('+255788811191', 'Hello!')

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
* **GitHub**: https://github.com/nexacon/nexacon-ruby-sdk
* **Issues**: https://github.com/nexacon/nexacon-ruby-sdk/issues
