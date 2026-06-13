Messaging
=========

The messaging service provides real-time communication capabilities including sending messages, message history, typing indicators, read receipts, and presence management.

For detailed API reference, see `API Reference <api-reference.html#messagingmanager>`_.

Features
--------

* **Send Messages** - Send text messages to users
* **Message History** - Retrieve message history with pagination
* **Typing Indicators** - Real-time typing status
* **Read Receipts** - Track when messages are read
* **Delivery Receipts** - Track when messages are delivered
* **Presence** - User online status

Quick Example
-------------

.. code-block:: dart

    final messagingManager = client.createMessagingManager();

    // Listen for incoming messages
    messagingManager.messageStream.listen((message) {
      print('Received: ${message['message']}');
    });

    // Send a message
    await messagingManager.sendMessage(
      to: '+255788811191',
      message: 'Hello!',
    );

See `Quick Start <quickstart.html>`_ for more examples.
