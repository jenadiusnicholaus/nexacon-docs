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

   final client = NexaconClient(
     apiKey: 'your_api_key',
     secretKey: 'your_secret_key',
   );

**Authentication**

Authenticate users with their credentials:

.. code-block:: dart

   final token = await client.auth.login(
     username: 'user@example.com',
     password: 'password',
   );

**Making a Call**

.. code-block:: dart

   final callManager = await client.createCallManager(
     nxtoken: token['token'],
     nxid: token['jid'],
     wsUrl: token['nxws'],
   );

   await callManager.initiateCall(
     to: '+255788811191',
     callType: 'video',
   );

.. note::
   For real-time chat messaging (text messages, typing indicators, presence), use the separate `Nexacon Messaging SDK <https://nexacon-messaging.readthedocs.io/>`_.

Next Steps
----------

* `Installation Guide <installation.html>`_ - Detailed installation instructions
* `Authentication Guide <guides/authentication.html>`_ - Learn about authentication
* `API Reference <flutter-sdk/api-reference.html>`_ - Explore the Flutter SDK API
* `Best Practices <guides/best-practices.html>`_ - Follow recommended practices
