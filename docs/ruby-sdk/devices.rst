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

.. code-block:: ruby

    # Register device for push notifications
    client.devices.register('device_fcm_token', 'android')
