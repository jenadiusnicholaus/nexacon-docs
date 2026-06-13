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

.. code-block:: python

    # Get user presence
    presence = client.presence.get_status('+255788811191')
    print('Online:', presence['online'])

    # Get last seen
    last_seen = client.presence.get_last_seen('+255788811191')
    print('Last seen:', last_seen['timestamp'])
