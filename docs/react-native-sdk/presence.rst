Presence
========

The presence service provides functionality for checking user online status and last seen information.

For detailed API reference, see `API Reference <api-reference.html#presence>`_.

Features
--------

* **Get Status** - Check if a user is online
* **Get Last Seen** - Get the last seen timestamp

Quick Example
-------------

.. code-block:: typescript

    // Get user presence
    const presence = await client.presence.getStatus('+255788811191');
    console.log('Online:', presence.online);

    // Get last seen
    const lastSeen = await client.presence.getLastSeen('+255788811191');
    console.log('Last seen:', lastSeen.timestamp);
