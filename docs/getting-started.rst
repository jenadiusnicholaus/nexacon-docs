Getting Started
===============

This guide will help you get started with the Nexacon Flutter SDK for audio/video calling.

Choose Your Platform
--------------------

.. grid:: 2

   .. grid-item-card:: Flutter
      :columns: 6
      :link: flutter-sdk/index.html
      :link-type: doc

      Cross-platform audio/video calling for Android, iOS, Linux, macOS, Web, and Windows.

.. note::
   Additional SDKs for other platforms are in development and will be added here once tested and stable.

Prerequisites
-------------

Before using the Nexacon Flutter SDK, you will need:

* **Nexacon API Key** - Contact Nexacon to obtain your API key and secret
* **Flutter SDK** - Version 3.0.0 or higher
* **Dart SDK** - Version 3.0.0 or higher
* **Account** - A Nexacon account for testing and development

First Steps
-----------

1. **Install the SDK** - Follow the `installation guide <installation.html>`_
2. **Initialize the client** - Set up the Nexacon client with your API credentials
3. **Authenticate** - Implement user authentication
4. **Start making calls** - Integrate audio/video calling into your app

Common Concepts
---------------

**Client Initialization**

.. code-block:: dart

   final sdk = NexaconSDK(
     apiKey: 'your_api_key',
     secretKey: 'your_secret_key',
   );

**Authentication**

The SDK handles authentication internally. Just provide your username when making a call:

.. code-block:: dart

   await sdk.startCall(
     to: '+255788811191',
     username: '+255123456789',
     audio: true,
     video: false,
   );

**Making a Call**

.. code-block:: dart

   sdk.onCallStateChanged = (state) => print('Call state: $state');
   sdk.onIncomingCall = (caller) => print('Incoming from: $caller');
   sdk.onCallEnded = (reason) => print('Call ended: $reason');

   await sdk.startCall(
     to: '+255788811191',
     username: '+255123456789',
     audio: true,
     video: false,
   );

.. note::
   For real-time chat messaging (text messages, typing indicators, presence), use the separate `Nexacon Messaging SDK <https://nexacon-messaging.readthedocs.io/>`_.

Next Steps
----------

* `Installation Guide <installation.html>`_ - Detailed installation instructions
* `Authentication Guide <guides/authentication.html>`_ - Learn about authentication
* `API Reference <flutter-sdk/api-reference.html>`_ - Explore the Flutter SDK API
* `Best Practices <guides/best-practices.html>`_ - Follow recommended practices
