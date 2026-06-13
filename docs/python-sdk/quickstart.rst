Python SDK Quick Start
=====================

Get up and running with the Nexacon Python SDK in minutes.

Initialize the Client
---------------------

.. code-block:: python

    from nexacon_sdk import NexaconClient

    client = NexaconClient(
        api_key='your_api_key',
        secret_key='your_secret_key'
    )

Available Services
------------------

Once the client is initialized, all services are available:

.. code-block:: python

    client.auth        # Authentication and token management
    client.messaging   # Send messages and manage contacts
    client.calls       # Audio/video calls
    client.devices     # Device registration for push notifications
    client.rooms       # Group chat rooms
    client.presence    # User presence and online status

Authentication
--------------

.. code-block:: python

    # Set the NX token (obtained from Nexacon dashboard)
    client.set_token('your_nx_token')

    # Generate XMPP token for real-time features
    nx_response = client.auth.generate_xmpp_token(
        username='+255788811191'
    )

    print('XMPP token:', nx_response['token'])
    print('JID:', nx_response['jid'])

Messaging
---------

.. code-block:: python

    # Send a message
    client.messaging.send(
        to='+255788811191',
        message='Hello!'
    )

    # Get message history
    messages = client.messaging.get_history(
        recipient='+255788811191',
        page=1,
        page_size=50
    )

    print('Messages:', messages['messages'])

Calls
-----

.. code-block:: python

    # Initiate a video call
    call = client.calls.initiate_call(
        to='+255788811191',
        call_type='video',
        room='my-room'
    )

    print('Call ID:', call['call_id'])

    # End the call
    client.calls.end_call(call['call_id'])

Device Registration
-------------------

.. code-block:: python

    # Register device for push notifications
    client.devices.register(
        fcm_token='device_fcm_token',
        platform='android'
    )

Presence
--------

.. code-block:: python

    # Get user presence
    presence = client.presence.get_status('+255788811191')
    print('Online:', presence['online'])

    # Get last seen
    last_seen = client.presence.get_last_seen('+255788811191')
    print('Last seen:', last_seen['timestamp'])

Complete Example
----------------

.. code-block:: python

    from nexacon_sdk import NexaconClient

    def main():
        # Initialize client
        client = NexaconClient(
            api_key='your_api_key',
            secret_key='your_secret_key'
        )

        # Set NX token (obtained from Nexacon dashboard)
        client.set_token('your_nx_token')

        # Generate XMPP token for real-time features
        nx_response = client.auth.generate_xmpp_token(
            username='+255788811191'
        )

        # Send message
        client.messaging.send(
            to='+255788811191',
            message='Hello from Python!'
        )

        # Make a call
        call = client.calls.initiate_call(
            to='+255788811191',
            call_type='video',
            room='my-room'
        )

        print('Call initiated:', call['call_id'])

    if __name__ == '__main__':
        main()

Next Steps
----------

* `API Reference <api-reference.html>`_ - Detailed API documentation
* `Messaging <messaging.html>`_ - Messaging features
* `Calls <calls.html>`_ - Calling features
* `Best Practices <../guides/best-practices.html>`_ - Recommended practices
