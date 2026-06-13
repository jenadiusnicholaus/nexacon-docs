React Native SDK API Reference
================================

This section provides detailed API reference for the Nexacon React Native SDK.

NexaconClient
-------------

.. js:class:: NexaconClient

    Main client class for interacting with the Nexacon API.

.. js:method:: NexaconClient(config)

    Initialize a new NexaconClient instance.

    :param config: Configuration object
    :type config: Object
    :param config.apiKey: API key for authentication
    :type config.apiKey: string
    :param config.secretKey: Secret key for authentication
    :type config.secretKey: string
    :param config.baseUrl: Base URL for API requests (default: https://nxservice.quantumvision-tech.com/api/v1.0)
    :type config.baseUrl: string
    :param config.timeout: Request timeout in milliseconds (default: 30000)
    :type config.timeout: number

.. js:method:: setToken(token)

    Set the authentication token for subsequent requests.

    :param token: Authentication token
    :type token: string

.. js:method:: getToken()

    Get the current authentication token.

    :returns: Current authentication token or null
    :rtype: string|null

Auth
----

.. js:class:: Auth

    Authentication service for user login and token management.

.. js:method:: Auth.login(credentials)

    Login a user with username and password.

    :param credentials: Login credentials
    :type credentials: Object
    :param credentials.username: User's username or phone number
    :type credentials.username: string
    :param credentials.password: User's password
    :type credentials.password: string
    :returns: Authentication response with access token
    :rtype: Promise<Object>

.. js:method:: Auth.refreshToken(refreshToken)

    Refresh an expired access token using a refresh token.

    :param refreshToken: Refresh token
    :type refreshToken: string
    :returns: New authentication response
    :rtype: Promise<Object>

.. js:method:: Auth.logout()

    Logout the current user and invalidate the token.

    :returns: Logout response
    :rtype: Promise<Object>

Messaging
---------

.. js:class:: Messaging

    Messaging service for sending and receiving messages.

.. js:method:: Messaging.send(message)

    Send a message to a recipient.

    :param message: Message object
    :type message: Object
    :param message.to: Recipient's phone number or JID
    :type message.to: string
    :param message.message: Message content
    :type message.message: string
    :param message.messageType: Message type (default: 'chat')
    :type message.messageType: string
    :returns: Send message response
    :rtype: Promise<Object>

.. js:method:: Messaging.getHistory(params)

    Get message history for a recipient.

    :param params: Query parameters
    :type params: Object
    :param params.recipient: Recipient's phone number or JID
    :type params.recipient: string
    :param params.page: Page number (default: 1)
    :type params.page: number
    :param params.pageSize: Number of messages per page (default: 50)
    :type params.pageSize: number
    :returns: Message history
    :rtype: Promise<Object>

Calls
-----

.. js:class:: Calls

    Calling service for audio/video calls.

.. js:method:: Calls.initiateCall(params)

    Initiate a call to a recipient.

    :param params: Call parameters
    :type params: Object
    :param params.to: Recipient's phone number
    :type params.to: string
    :param params.callType: Type of call ('audio' or 'video')
    :type params.callType: string
    :param params.room: Room ID for the call
    :type params.room: string
    :returns: Call information
    :rtype: Promise<Object>

.. js:method:: Calls.endCall(callId)

    End an active call.

    :param callId: Call ID
    :type callId: string
    :returns: End call response
    :rtype: Promise<Object>

Devices
-------

.. js:class:: Devices

    Device registration service for push notifications.

.. js:method:: Devices.register(device)

    Register a device for push notifications.

    :param device: Device information
    :type device: Object
    :param device.fcmToken: FCM token for the device
    :type device.fcmToken: string
    :param device.platform: Platform ('android', 'ios', or 'web')
    :type device.platform: string
    :param device.deviceName: Device name (optional)
    :type device.deviceName: string
    :returns: Registration response
    :rtype: Promise<Object>

.. js:method:: Devices.unregister(fcmToken)

    Unregister a device from push notifications.

    :param fcmToken: FCM token
    :type fcmToken: string
    :returns: Unregistration response
    :rtype: Promise<Object>

.. js:method:: Devices.listDevices()

    List all registered devices.

    :returns: List of devices
    :rtype: Promise<Object>

Rooms
-----

.. js:class:: Rooms

    Room management service for group chat rooms.

.. js:method:: Rooms.create(params)

    Create a new group chat room.

    :param params: Room parameters
    :type params: Object
    :param params.name: Room name
    :type params.name: string
    :param params.description: Room description (optional)
    :type params.description: string
    :param params.members: Array of member phone numbers
    :type params.members: string[]
    :returns: Room information
    :rtype: Promise<Object>

.. js:method:: Rooms.list(params)

    List available rooms.

    :param params: Query parameters (optional)
    :type params: Object
    :param params.page: Page number (default: 1)
    :type params.page: number
    :param params.pageSize: Number of rooms per page (default: 50)
    :type params.pageSize: number
    :returns: List of rooms
    :rtype: Promise<Object>

Presence
--------

.. js:class:: Presence

    Presence service for checking user online status.

.. js:method:: Presence.getStatus(userId)

    Get the presence status of a user.

    :param userId: User's phone number or JID
    :type userId: string
    :returns: Presence information
    :rtype: Promise<Object>

.. js:method:: Presence.getLastSeen(userId)

    Get the last seen timestamp of a user.

    :param userId: User's phone number or JID
    :type userId: string
    :returns: Last seen information
    :rtype: Promise<Object>
