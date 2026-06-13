Presence
========

The presence service provides functionality for checking user online status and last seen information.

For detailed API reference, see `API Reference <api-reference.html#presence>`_.

Features
--------

* **Get Status** - Check if a user is online
* **Get Last Seen** - Get the last seen timestamp
* **Presence Streams** - Real-time presence updates

Quick Example
-------------

.. code-block:: dart

    // Get user presence
    final presence = await client.presence.getStatus('+255788811191');
    print('Online: ${presence['online']}');

    // Get last seen
    final lastSeen = await client.presence.getLastSeen('+255788811191');
    print('Last seen: ${lastSeen['timestamp']}');
