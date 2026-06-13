React Native SDK Quick Start
=============================

Get up and running with the Nexacon React Native SDK in minutes.

Initialize the Client
---------------------

.. code-block:: typescript

    import { NexaconClient } from 'nexacon-react-native-sdk';

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

    // Set the NX token (obtained from Nexacon dashboard)
    client.setToken('your_nx_token');

    // Generate XMPP token for real-time features
    const nxResponse = await client.auth.generateXMPPToken({
      username: '+255788811191',
    });

    console.log('XMPP token:', nxResponse.token);
    console.log('JID:', nxResponse.jid);

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

Device Registration
-------------------

.. code-block:: typescript

    // Register device for push notifications
    await client.devices.register({
      fcmToken: 'device_fcm_token',
      platform: 'android',
      deviceName: 'My Device',
    });

Presence
--------

.. code-block:: typescript

    // Get user presence
    const presence = await client.presence.getStatus('+255788811191');
    console.log('Online:', presence.online);
    console.log('Status:', presence.status);

Complete Example
----------------

.. code-block:: typescript

    import React, { useEffect } from 'react';
    import { NexaconClient } from 'nexacon-react-native-sdk';

    function App() {
      useEffect(() => {
        async function init() {
          const client = new NexaconClient({
            apiKey: 'your_api_key',
            secretKey: 'your_secret_key',
          });

          // Set NX token (obtained from Nexacon dashboard)
          client.setToken('your_nx_token');

          // Generate XMPP token for real-time features
          const nxResponse = await client.auth.generateXMPPToken({
            username: '+255788811191',
          });

          await client.messaging.send({
            to: '+255788811191',
            message: 'Hello from React Native!',
          });
        }

        init();
      }, []);

      return null;
    }

Next Steps
----------

* `API Reference <api-reference.html>`_ - Detailed API documentation
* `Messaging <messaging.html>`_ - Messaging features
* `Calls <calls.html>`_ - Calling features
* `Best Practices <../guides/best-practices.html>`_ - Recommended practices
