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

.. code-block:: go

    // Create a room
    room, err := client.Rooms.Create("Project Team", []string{"+255788811191", "+255788811192"})

    // List rooms
    rooms, err := client.Rooms.List()
