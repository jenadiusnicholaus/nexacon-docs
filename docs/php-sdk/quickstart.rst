PHP SDK Quick Start
==================

Get up and running with the Nexacon PHP SDK in minutes.

Initialize the Client
---------------------

.. code-block:: php

    <?php
    require 'vendor/autoload.php';
    use Nexacon\SDK\NexaconClient;

    $client = new NexaconClient('your_api_key', 'your_secret_key');

Available Services
------------------

Once the client is initialized, all services are available:

.. code-block:: php

    $client->auth        // Authentication and token management
    $client->messaging   // Send messages and manage contacts
    $client->calls       // Audio/video calls
    $client->devices     // Device registration for push notifications
    $client->rooms       // Group chat rooms
    $client->presence    // User presence and online status

Authentication
--------------

.. code-block:: php

    // Generate XMPP token for real-time features
    $nxResponse = $client->auth->generateXMPPToken('+255788811191');

    echo 'XMPP token: ' . $nxResponse['token'];
    echo 'JID: ' . $nxResponse['jid'];
    echo 'WebSocket URL: ' . $nxResponse['nxws'];

Messaging
---------

.. code-block:: php

    // Send a message
    $client->messaging->send('+255788811191', 'Hello!');

    // Get message history
    $messages = $client->messaging->getHistory('+255788811191', 1, 50);

    echo 'Messages: ' . print_r($messages['messages'], true);

Calls
-----

.. code-block:: php

    // Initiate a video call
    $call = $client->calls->initiateCall('+255788811191', 'video', 'my-room');

    echo 'Call ID: ' . $call['call_id'];

    // End the call
    $client->calls->endCall($call['call_id']);

Device Registration
-------------------

.. code-block:: php

    // Register device for push notifications
    $client->devices->register('device_fcm_token', 'android');

Presence
--------

.. code-block:: php

    // Get user presence
    $presence = $client->presence->getStatus('+255788811191');
    echo 'Online: ' . $presence['online'];

    // Get last seen
    $lastSeen = $client->presence->getLastSeen('+255788811191');
    echo 'Last seen: ' . $lastSeen['timestamp'];

Complete Example
----------------

.. code-block:: php

    <?php
    require 'vendor/autoload.php';
    use Nexacon\SDK\NexaconClient;

    // Initialize client
    $client = new NexaconClient('your_api_key', 'your_secret_key');

    // Generate XMPP token for real-time features
    $nxResponse = $client->auth->generateXMPPToken('+255788811191');

    // Send message
    $client->messaging->send('+255788811191', 'Hello from PHP!');

    // Make a call
    $call = $client->calls->initiateCall('+255788811191', 'video', 'my-room');

    echo 'Call initiated: ' . $call['call_id'];

Next Steps
----------

* `API Reference <api-reference.html>`_ - Detailed API documentation
* `Messaging <messaging.html>`_ - Messaging features
* `Calls <calls.html>`_ - Calling features
* `Best Practices <../guides/best-practices.html>`_ - Recommended practices
