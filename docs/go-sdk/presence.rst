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

.. code-block:: go

    // Get user presence
    presence, err := client.Presence.GetStatus("+255788811191")
    fmt.Println("Online:", presence.Online)

    // Get last seen
    lastSeen, err := client.Presence.GetLastSeen("+255788811191")
    fmt.Println("Last seen:", lastSeen.Timestamp)
