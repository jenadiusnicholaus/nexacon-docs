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

.. code-block:: java

    // Get user presence
    Map<String, Object> presence = client.presence.getStatus("+255788811191");
    System.out.println("Online: " + presence.get("online"));

    // Get last seen
    Map<String, Object> lastSeen = client.presence.getLastSeen("+255788811191");
    System.out.println("Last seen: " + lastSeen.get("timestamp"));
