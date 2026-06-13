Messaging
=========

The messaging service provides real-time communication capabilities including sending messages and message history.

For detailed API reference, see `API Reference <api-reference.html#messaging>`_.

Features
--------

* **Send Messages** - Send text messages to users
* **Message History** - Retrieve message history with pagination

Quick Example
-------------

.. code-block:: java

    // Send a message
    client.messaging.send("+255788811191", "Hello!");

    // Get message history
    Map<String, Object> messages = client.messaging.getHistory("+255788811191", 1, 50);

See `Quick Start <quickstart.html>`_ for more examples.
