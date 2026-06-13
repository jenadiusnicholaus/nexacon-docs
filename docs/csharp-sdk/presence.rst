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

.. code-block:: csharp

    // Get user presence
    var presence = await client.Presence.GetStatusAsync("+255788811191");
    Console.WriteLine($"Online: {presence.Online}");

    // Get last seen
    var lastSeen = await client.Presence.GetLastSeenAsync("+255788811191");
    Console.WriteLine($"Last seen: {lastSeen.Timestamp}");
