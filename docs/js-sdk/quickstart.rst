JavaScript SDK Quick Start
=========================

Get up and running with the Nexacon JavaScript SDK in minutes.

Initialize the Client
---------------------

.. code-block:: typescript

    import { NexaconClient } from 'nexacon-sdk';

    const client = new NexaconClient({
      apiKey: 'your_api_key',
      secretKey: 'your_secret_key',
    });

Available Services
------------------

Once the client is initialized, all services are available:

.. code-block:: typescript

    client.auth        // Authentication and token management
    client.messaging   // Send messages and manage contacts
    client.calls       // Audio/video calls
    client.devices     // Device registration for push notifications
    client.rooms       // Group chat rooms
    client.presence    // User presence and online status

Authentication
--------------

.. code-block:: typescript

    // Login user
    const token = await client.auth.login({
      username: 'user@example.com',
      password: 'password',
    });

    console.log('Access token:', token.access_token);
    console.log('Refresh token:', token.refresh_token);

    // Set token for subsequent requests
    client.setToken(token.access_token);

Messaging
---------

.. code-block:: typescript

    // Send a message
    await client.messaging.send({
      to: '+255788811191',
      message: 'Hello!',
    });

    // Get message history
    const messages = await client.messaging.getHistory({
      recipient: '+255788811191',
      page: 1,
      pageSize: 50,
    });

    console.log('Messages:', messages.messages);

Calls
-----

.. code-block:: typescript

    // Initiate a video call
    const call = await client.calls.initiateCall({
      to: '+255788811191',
      callType: 'video',
      room: 'my-room',
    });

    console.log('Call ID:', call.callId);

    // End the call
    await client.calls.endCall(call.callId);

    // Get call history
    const history = await client.calls.getCallHistory({
      page: 1,
      pageSize: 50,
    });

    console.log('Calls:', history.calls);

Device Registration
-------------------

.. code-block:: typescript

    // Register device for push notifications
    await client.devices.register({
      fcmToken: 'device_fcm_token',
      platform: 'android',
    });

    // List devices
    const devices = await client.devices.listDevices();
    console.log('Devices:', devices);

Presence
--------

.. code-block:: typescript

    // Get user presence
    const presence = await client.presence.getStatus('+255788811191');
    console.log('Online:', presence.online);
    console.log('Status:', presence.status);

    // Get last seen
    const lastSeen = await client.presence.getLastSeen('+255788811191');
    console.log('Last seen:', lastSeen.timestamp);

Complete Example
----------------

.. code-block:: typescript

    import { NexaconClient } from 'nexacon-sdk';

    async function main() {
      // Initialize client
      const client = new NexaconClient({
        apiKey: 'your_api_key',
        secretKey: 'your_secret_key',
      });

      // Authenticate
      const token = await client.auth.login({
        username: 'user@example.com',
        password: 'password',
      });

      client.setToken(token.access_token);

      // Send message
      await client.messaging.send({
        to: '+255788811191',
        message: 'Hello from JavaScript!',
      });

      // Make a call
      const call = await client.calls.initiateCall({
        to: '+255788811191',
        callType: 'video',
        room: 'my-room',
      });

      console.log('Call initiated:', call.callId);
    }

    main();

Next Steps
----------

* `API Reference <api-reference.html>`_ - Detailed API documentation
* `Messaging <messaging.html>`_ - Messaging features
* `Calls <calls.html>`_ - Calling features
* `Best Practices <../guides/best-practices.html>`_ - Recommended practices
