Rooms
=====

The rooms service provides functionality for creating and managing group chat rooms.

For detailed API reference, see `API Reference <api-reference.html#rooms>`_.

Features
--------

* **Create Rooms** - Create group chat rooms
* **List Rooms** - View available rooms
* **Room Messages** - Get messages from rooms
* **Manage Members** - Add and remove room members

Quick Example
-------------

.. code-block:: dart

    // Create a room
    final room = await client.rooms.create(
      name: 'Project Team',
      members: ['+255788811191', '+255788811192'],
    );
