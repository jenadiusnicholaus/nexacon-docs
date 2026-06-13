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

.. code-block:: python

    # Send a message
    client.messaging.send(
        to='+255788811191',
        message='Hello!'
    )

    # Get message history
    messages = client.messaging.get_history(
        recipient='+255788811191',
        page=1,
        page_size=50
    )

See `Quick Start <quickstart.html>`_ for more examples.
