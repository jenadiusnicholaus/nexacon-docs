Java SDK
=========

The Nexacon Java SDK provides a comprehensive solution for integrating the Nexacon API into Java applications for Android and server-side use.

.. toctree::
   :maxdepth: 2
   :caption: Java SDK:

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

The Java SDK offers:

* **Java 8+ support** - Modern Java versions
* **Android support** - Native Android integration
* **Maven/Gradle** - Easy dependency management
* **Real-time messaging** - Message streams, typing indicators, read receipts
* **Audio/Video calling** - WebRTC-based P2P and group calls
* **Device management** - Push notification registration
* **Presence** - User online status and last seen

Installation
------------

**Maven**

.. code-block:: xml

    <dependency>
        <groupId>com.nexacon</groupId>
        <artifactId>nexacon-sdk</artifactId>
        <version>1.0.0</version>
    </dependency>

**Gradle**

.. code-block:: groovy

    implementation 'com.nexacon:nexacon-sdk:1.0.0'

See `Installation Guide <installation.html>`_ for detailed setup instructions.

Quick Start
-----------

.. code-block:: java

    import com.nexacon.sdk.NexaconClient;

    // Initialize client
    NexaconClient client = new NexaconClient(
        "your_api_key",
        "your_secret_key"
    );

    // Authenticate user
    Map<String, Object> token = client.auth.login(
        "user@example.com",
        "password"
    );

    // Send message
    client.messaging.send(
        "+255788811191",
        "Hello!"
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
     - Android 5.0+ (API 21+)
   * - JVM
     - ✅ Stable
     - Java 8+

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
* **GitHub**: https://github.com/nexacon/nexacon-java-sdk
* **Issues**: https://github.com/nexacon/nexacon-java-sdk/issues
