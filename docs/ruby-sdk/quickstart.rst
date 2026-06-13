Ruby SDK Quick Start
===================

Get up and running with the Nexacon Ruby SDK in minutes.

Initialize the Client
---------------------

.. code-block:: ruby

    require 'nexacon-sdk'

    client = NexaconClient.new('your_api_key', 'your_secret_key')

Available Services
------------------

Once the client is initialized, all services are available:

.. code-block:: ruby

    client.auth        # Authentication and token management
    client.messaging   # Send messages and manage contacts
    client.calls       # Audio/video calls
    client.devices     # Device registration for push notifications
    client.rooms       # Group chat rooms
    client.presence    # User presence and online status

Authentication
--------------

.. code-block:: ruby

    # Login user
    token = client.auth.login('user@example.com', 'password')

    puts "Access token: #{token['access_token']}"
    puts "Refresh token: #{token['refresh_token']}"

    # Set token for subsequent requests
    client.set_token(token['access_token'])

Messaging
---------

.. code-block:: ruby

    # Send a message
    client.messaging.send('+255788811191', 'Hello!')

    # Get message history
    messages = client.messaging.get_history('+255788811191', 1, 50)

    puts "Messages: #{messages['messages']}"

Calls
-----

.. code-block:: ruby

    # Initiate a video call
    call = client.calls.initiate_call('+255788811191', 'video', 'my-room')

    puts "Call ID: #{call['call_id']}"

    # End the call
    client.calls.end_call(call['call_id'])

Device Registration
-------------------

.. code-block:: ruby

    # Register device for push notifications
    client.devices.register('device_fcm_token', 'android')

Presence
--------

.. code-block:: ruby

    # Get user presence
    presence = client.presence.get_status('+255788811191')
    puts "Online: #{presence['online']}"

    # Get last seen
    last_seen = client.presence.get_last_seen('+255788811191')
    puts "Last seen: #{last_seen['timestamp']}"

Complete Example
----------------

.. code-block:: ruby

    require 'nexacon-sdk'

    # Initialize client
    client = NexaconClient.new('your_api_key', 'your_secret_key')

    # Authenticate
    token = client.auth.login('user@example.com', 'password')
    client.set_token(token['access_token'])

    # Send message
    client.messaging.send('+255788811191', 'Hello from Ruby!')

    # Make a call
    call = client.calls.initiate_call('+255788811191', 'video', 'my-room')

    puts "Call initiated: #{call['call_id']}"

Next Steps
----------

* `API Reference <api-reference.html>`_ - Detailed API documentation
* `Messaging <messaging.html>`_ - Messaging features
* `Calls <calls.html>`_ - Calling features
* `Best Practices <../guides/best-practices.html>`_ - Recommended practices
