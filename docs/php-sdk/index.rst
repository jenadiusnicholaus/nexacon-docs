PHP SDK
=======

The Nexacon PHP SDK provides a comprehensive solution for integrating the Nexacon API into PHP applications for web use.

.. toctree::
   :maxdepth: 2
   :caption: PHP SDK:

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

The PHP SDK offers:

* **PHP 7.4+ support** - Modern PHP versions
* **Composer** - Easy dependency management
* **Type hints** - Full type annotations
* **Real-time messaging** - Message streams, typing indicators, read receipts
* **Audio/Video calling** - WebRTC-based P2P and group calls
* **Device management** - Push notification registration
* **Presence** - User online status and last seen

Installation
------------

.. code-block:: bash

    composer require nexacon/sdk

See `Installation Guide <installation.html>`_ for detailed setup instructions.

Quick Start
-----------

.. code-block:: php

    <?php
    require 'vendor/autoload.php';
    use Nexacon\SDK\NexaconClient;

    // Initialize client
    $client = new NexaconClient('your_api_key', 'your_secret_key');

    // Authenticate user
    $token = $client->auth->login('user@example.com', 'password');

    // Send message
    $client->messaging->send('+255788811191', 'Hello!');

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
* **GitHub**: https://github.com/nexacon/nexacon-php-sdk
* **Issues**: https://github.com/nexacon/nexacon-php-sdk/issues
