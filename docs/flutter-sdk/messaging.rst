Messaging
=========

.. note::
   Real-time chat messaging is handled by the separate **Nexacon Messaging SDK** (``nexacon_messaging``), not the Flutter Call SDK.

   The Nexacon Messaging SDK provides:

   * Send and receive text messages over WebSocket
   * Message history with offset-based pagination
   * Typing indicators (XEP-0085)
   * Delivery and read receipts (XEP-0184)
   * Presence tracking (online/away/busy/offline)
   * Auto-reconnect with exponential backoff

**Installation**

.. code-block:: bash

    flutter pub add nexacon_messaging

**Documentation**

Full documentation is available at `nexacon-messaging.readthedocs.io <https://nexacon-messaging.readthedocs.io/>`_.

**Quick Example**

.. code-block:: dart

    import 'package:nexacon_messaging/nexacon_messaging.dart';

    final messaging = NexaconMessaging(
      apiKey: 'your_api_key',
      secretKey: 'your_secret_key',
    );

    await messaging.connectWithToken(
      username: '+255123456789',
      apiKey: 'your_api_key',
      secretKey: 'your_secret_key',
    );

    messaging.messageStream.listen((msg) {
      print('From ${msg.from}: ${msg.body}');
    });

    await messaging.sendMessage(
      to: '+255987654321',
      message: 'Hello!',
    );

See `Nexacon Messaging SDK docs <https://nexacon-messaging.readthedocs.io/>`_ for complete guides and API reference.
