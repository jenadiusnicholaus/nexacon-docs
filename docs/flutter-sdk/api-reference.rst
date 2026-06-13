Flutter SDK API Reference
=========================

This section provides detailed API reference for the Nexacon Flutter SDK.

NexaconClient
-------------

.. dart:class:: NexaconClient

    Main client class for interacting with the Nexacon API.

.. dart:method:: NexaconClient({required String apiKey, required String secretKey, String? baseUrl})

    Initialize a new NexaconClient instance.

    :param apiKey: API key for authentication
    :type apiKey: String
    :param secretKey: Secret key for authentication
    :type secretKey: String
    :param baseUrl: Base URL for API requests (default: https://nxservice.quantumvision-tech.com/api/v1.0)
    :type baseUrl: String?

.. dart:method:: Future<Map<String, dynamic>> auth.login({required String username, required String password})

    Login a user with username and password.

    :param username: User's username or phone number
    :type username: String
    :param password: User's password
    :type password: String
    :returns: Authentication response with token
    :rtype: Future<Map<String, dynamic>>

.. dart:method:: Future<Map<String, dynamic>> auth.generateXMPPToken({required String username})

    Generate XMPP token for signaling.

    :param username: User's username or phone number
    :type username: String
    :returns: XMPP token response
    :rtype: Future<Map<String, dynamic>>

.. dart:method:: MessagingManager createMessagingManager()

    Create a messaging manager instance.

    :returns: MessagingManager instance
    :rtype: MessagingManager

.. dart:method:: Future<CallManager> createCallManager({required String nxtoken, required String nxid, required String wsUrl, Function(String)? onCallStateChanged, Function(String)? onIncomingCall})

    Create a call manager instance.

    :param nxtoken: NX token for signaling
    :type nxtoken: String
    :param nxid: NX ID (JID)
    :type nxid: String
    :param wsUrl: WebSocket URL for signaling
    :type wsUrl: String
    :param onCallStateChanged: Callback for call state changes
    :type onCallStateChanged: Function(String)?
    :param onIncomingCall: Callback for incoming calls
    :type onIncomingCall: Function(String)?
    :returns: CallManager instance
    :rtype: Future<CallManager>

MessagingManager
---------------

.. dart:class:: MessagingManager

    Messaging service for sending and receiving messages.

.. dart:method:: Stream<Map<String, dynamic>> get messageStream

    Stream of incoming messages.

    :returns: Message stream
    :rtype: Stream<Map<String, dynamic>>

.. dart:method:: Stream<Map<String, dynamic>> get typingStream

    Stream of typing indicators.

    :returns: Typing stream
    :rtype: Stream<Map<String, dynamic>>

.. dart:method:: Stream<Map<String, dynamic>> get readReceiptStream

    Stream of read receipts.

    :returns: Read receipt stream
    :rtype: Stream<Map<String, dynamic>>

.. dart:method:: Stream<Map<String, dynamic>> get deliveryReceiptStream

    Stream of delivery receipts.

    :returns: Delivery receipt stream
    :rtype: Stream<Map<String, dynamic>>

.. dart:method:: Stream<Map<String, dynamic>> get presenceStream

    Stream of presence updates.

    :returns: Presence stream
    :rtype: Stream<Map<String, dynamic>>

.. dart:method:: Future<void> sendMessage({required String to, required String message, String messageType = 'chat'})

    Send a message to a recipient.

    :param to: Recipient's phone number or JID
    :type to: String
    :param message: Message content
    :type message: String
    :param messageType: Message type (default: 'chat')
    :type messageType: String
    :returns: Future
    :rtype: Future<void>

.. dart:method:: Future<Map<String, dynamic>> getHistory({required String recipient, int page = 1, int pageSize = 50})

    Get message history for a recipient.

    :param recipient: Recipient's phone number or JID
    :type recipient: String
    :param page: Page number (default: 1)
    :type page: int
    :param pageSize: Number of messages per page (default: 50)
    :type pageSize: int
    :returns: Message history
    :rtype: Future<Map<String, dynamic>>

CallManager
-----------

.. dart:class:: CallManager

    Calling service for audio/video calls.

.. dart:method:: Future<void> initiateCall({required String to, required String callType, String? room})

    Initiate a call to a recipient.

    :param to: Recipient's phone number
    :type to: String
    :param callType: Type of call ('audio' or 'video')
    :type callType: String
    :param room: Room ID for the call
    :type room: String?
    :returns: Future
    :rtype: Future<void>

.. dart:method:: Future<void> endCall()

    End the active call.

    :returns: Future
    :rtype: Future<void>

.. dart:method:: Future<void> muteAudio(bool muted)

    Mute/unmute audio.

    :param muted: Whether to mute audio
    :type muted: bool
    :returns: Future
    :rtype: Future<void>

.. dart:method:: Future<void> switchCamera()

    Switch between front and back camera.

    :returns: Future
    :rtype: Future<void>

.. dart:method:: Future<void> setSpeakerphone(bool enabled)

    Enable/disable speakerphone.

    :param enabled: Whether to enable speakerphone
    :type enabled: bool
    :returns: Future
    :rtype: Future<void>

Devices
-------

.. dart:method:: Future<void> devices.register({required String fcmToken, required String platform, String? deviceId})

    Register a device for push notifications.

    :param fcmToken: FCM token for the device
    :type fcmToken: String
    :param platform: Platform ('android', 'ios', or 'web')
    :type platform: String
    :param deviceId: Unique device identifier
    :type deviceId: String?
    :returns: Future
    :rtype: Future<void>

.. dart:method:: Future<void> devices.unregister(String fcmToken)

    Unregister a device from push notifications.

    :param fcmToken: FCM token
    :type fcmToken: String
    :returns: Future
    :rtype: Future<void>

Rooms
-----

.. dart:method:: Future<Map<String, dynamic>> rooms.create({required String name, String? description, required List<String> members})

    Create a new group chat room.

    :param name: Room name
    :type name: String
    :param description: Room description
    :type description: String?
    :param members: Array of member phone numbers
    :type members: List<String>
    :returns: Room information
    :rtype: Future<Map<String, dynamic>>

.. dart:method:: Future<Map<String, dynamic>> rooms.list({int page = 1, int pageSize = 50})

    List available rooms.

    :param page: Page number (default: 1)
    :type page: int
    :param pageSize: Number of rooms per page (default: 50)
    :type pageSize: int
    :returns: List of rooms
    :rtype: Future<Map<String, dynamic>>

Presence
--------

.. dart:method:: Future<Map<String, dynamic>> presence.getStatus(String userId)

    Get the presence status of a user.

    :param userId: User's phone number or JID
    :type userId: String
    :returns: Presence information
    :rtype: Future<Map<String, dynamic>>

.. dart:method:: Future<Map<String, dynamic>> presence.getLastSeen(String userId)

    Get the last seen timestamp of a user.

    :param userId: User's phone number or JID
    :type userId: String
    :returns: Last seen information
    :rtype: Future<Map<String, dynamic>>

FoldStateService
----------------

.. dart:class:: FoldStateService

    Service for detecting foldable device state changes.

.. dart:method:: Stream<FoldState> get foldStateStream

    Stream of fold state changes.

    :returns: Fold state stream
    :rtype: Stream<FoldState>

.. dart:method:: FoldState get currentState

    Get the current fold state.

    :returns: Current fold state
    :rtype: FoldState

.. dart:method:: bool get isFolded

    Check if device is folded.

    :returns: True if folded
    :rtype: bool

.. dart:method:: bool get isFlat

    Check if device is flat.

    :returns: True if flat
    :rtype: bool

.. dart:method:: bool get isHalfOpen

    Check if device is half-open.

    :returns: True if half-open
    :rtype: bool

FoldState Enum
--------------

.. dart:enum:: FoldState

    Enum representing foldable device states.

.. dart:enum-member:: FoldState.flat

    Device is completely flat.

.. dart:enum-member:: FoldState.folded

    Device is completely folded.

.. dart:enum-member:: FoldState.halfOpen

    Device is half-open.

.. dart:enum-member:: FoldState.unknown

    Fold state is unknown.
