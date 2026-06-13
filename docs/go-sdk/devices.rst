Devices
=======

The devices service provides functionality for registering and managing devices for push notifications.

For detailed API reference, see `API Reference <api-reference.html#devices>`_.

Features
--------

* **Register Device** - Register device for push notifications
* **Unregister Device** - Remove device from push notifications
* **List Devices** - View all registered devices

Quick Example
-------------

.. code-block:: go

    // Register device for push notifications
    err := client.Devices.Register("device_fcm_token", "android")
