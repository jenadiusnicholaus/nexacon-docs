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
    :param baseUrl: Base URL for API requests (default: your-domain.com/api/v1.0)
    :type baseUrl: String?

.. dart:method:: Future<Map<String, dynamic>> auth.login({required String username, required String password})

    Login a user with username and password.

    :param username: User's username or phone number
    :type username: String
    :param password: User's password
    :type password: String
    :returns: Authentication response with token
    :rtype: Future<Map<String, dynamic>>

.. dart:method:: Future<Map<String, dynamic>> auth.generateNxToken({required String username})

    Generate NX token for signaling.

    :param username: User's username or phone number
    :type username: String
    :returns: NX token response
    :rtype: Future<Map<String, dynamic>>

.. dart:method:: MessagingManager createMessagingManager()

    Create a messaging manager instance.

    .. note::
       This is a basic messaging manager. For full-featured chat (message history, pagination, presence), use the separate `Nexacon Messaging SDK <https://nexacon-messaging.readthedocs.io/>`_.

    :returns: MessagingManager instance
    :rtype: MessagingManager

.. dart:method:: Future<CallManager> createCallManager({String? nxtoken, String? nxid, String? wsUrl, String? name, Function(CallState)? onCallStateChanged, Function(String)? onIncomingCall, Function(String)? onCallEnded, Function(String)? onError, Function(MediaStream)? onLocalStream, Function(MediaStream)? onRemoteStream, Function()? onOtherUserJoined, Function()? onOtherUserLeft})

    Create a call manager instance.

    :param nxtoken: NX token for signaling
    :type nxtoken: String?
    :param nxid: NX ID (JID)
    :type nxid: String?
    :param wsUrl: WebSocket URL for signaling
    :type wsUrl: String?
    :param name: Display name for the caller
    :type name: String?
    :param onCallStateChanged: Callback for call state changes
    :type onCallStateChanged: Function(CallState)?
    :param onIncomingCall: Callback for incoming calls (caller name)
    :type onIncomingCall: Function(String)?
    :param onCallEnded: Callback for call ended (reason)
    :type onCallEnded: Function(String)?
    :param onError: Callback for errors
    :type onError: Function(String)?
    :param onLocalStream: Callback for local media stream
    :type onLocalStream: Function(MediaStream)?
    :param onRemoteStream: Callback for remote media stream
    :type onRemoteStream: Function(MediaStream)?
    :param onOtherUserJoined: Callback when remote peer joins
    :type onOtherUserJoined: Function()?
    :param onOtherUserLeft: Callback when remote peer leaves
    :type onOtherUserLeft: Function()?
    :returns: CallManager instance
    :rtype: Future<CallManager>

MessagingManager
---------------

.. dart:class:: MessagingManager

    Basic messaging service for sending and receiving messages.

    .. note::
       For full-featured chat messaging (message history with pagination, presence, typing indicators, delivery receipts), use the separate `Nexacon Messaging SDK <https://nexacon-messaging.readthedocs.io/>`_.

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

.. dart:method:: void sendMessage({required String to, required String message, String messageType = 'chat'})

    Send a message to a recipient.

    :param to: Recipient's phone number or JID
    :type to: String
    :param message: Message content
    :type message: String
    :param messageType: Message type (default: 'chat')
    :type messageType: String

.. dart:method:: void sendTypingIndicator(String to, {bool isTyping = true})

    Send a typing indicator.

    :param to: Recipient's phone number or JID
    :type to: String
    :param isTyping: Whether the user is typing
    :type isTyping: bool

.. dart:method:: void sendReadReceipt(String to, String messageId)

    Send a read receipt.

    :param to: Recipient's phone number or JID
    :type to: String
    :param messageId: Message ID to mark as read
    :type messageId: String

.. dart:method:: void dispose()

    Clean up stream controllers.

CallManager
-----------

.. dart:class:: CallManager

    Calling service for P2P audio/video calls using WebRTC.

CallState Enum
^^^^^^^^^^^^^^

.. dart:enum:: CallState

    Enum representing call states.

    * ``CallState.idle`` - No active call
    * ``CallState.calling`` - Outgoing call in progress
    * ``CallState.incoming`` - Incoming call waiting to be accepted
    * ``CallState.connected`` - Call is connected
    * ``CallState.ended`` - Call has ended

.. dart:method:: Future<bool> initialize({required String nxid, required String nxtoken, required String wsUrl, String? name})

    Initialize the call manager with NX credentials.

    :param nxid: NX ID (JID)
    :type nxid: String
    :param nxtoken: NX token for authentication
    :type nxtoken: String
    :param wsUrl: WebSocket URL for signaling
    :type wsUrl: String
    :param name: Display name (defaults to JID username)
    :type name: String?
    :returns: Whether initialization succeeded
    :rtype: Future<bool>

.. dart:method:: Future<void> initiateCall({required String to, bool audio = true, bool video = true, String? roomId})

    Initiate an outgoing P2P call.

    :param to: Recipient's phone number or JID
    :type to: String
    :param audio: Whether to include audio (default: true)
    :type audio: bool
    :param video: Whether to include video (default: true)
    :type video: bool
    :param roomId: Custom room ID (auto-generated if omitted)
    :type roomId: String?
    :returns: Future
    :rtype: Future<void>

.. dart:method:: void prepareIncomingCall({required String roomId, required String callerNxId, String callerName = 'Unknown'})

    Inject incoming call state from push notification data.

    :param roomId: Room ID from the push payload
    :type roomId: String
    :param callerNxId: Caller's NX ID from the push payload
    :type callerNxId: String
    :param callerName: Caller's display name
    :type callerName: String

.. dart:method:: Future<void> acceptCall({bool audio = true, bool video = true})

    Accept an incoming call.

    :param audio: Whether to include audio (default: true)
    :type audio: bool
    :param video: Whether to include video (default: true)
    :type video: bool
    :returns: Future
    :rtype: Future<void>

.. dart:method:: void rejectCall()

    Reject an incoming call.

.. dart:method:: Future<void> endCall()

    End the current call.

    :returns: Future
    :rtype: Future<void>

.. dart:method:: void toggleAudio(bool enabled)

    Enable/disable audio (mute).

    :param enabled: Whether audio is enabled
    :type enabled: bool

.. dart:method:: void toggleVideo(bool enabled)

    Enable/disable video.

    :param enabled: Whether video is enabled
    :type enabled: bool

.. dart:method:: Future<void> switchCamera()

    Switch between front and back camera.

.. dart:method:: void setVideoQuality({int width = 1280, int height = 720, int fps = 30})

    Set video resolution and frame rate.

    :param width: Video width in pixels (default: 1280)
    :type width: int
    :param height: Video height in pixels (default: 720)
    :type height: int
    :param fps: Frame rate (default: 30)
    :type fps: int

.. dart:method:: void setAudioBitrate(int kbps)

    Set audio bitrate.

    :param kbps: Bitrate in kbps
    :type kbps: int

.. dart:method:: void setVideoBitrate(int kbps)

    Set video bitrate.

    :param kbps: Bitrate in kbps
    :type kbps: int

.. dart:method:: void startCallStatsCollection({Duration interval = const Duration(seconds: 2)})

    Start collecting WebRTC call statistics.

    :param interval: Polling interval for stats
    :type interval: Duration

.. dart:method:: CallState get callState

    Get current call state.

    :returns: Current call state
    :rtype: CallState

.. dart:method:: Duration get callDuration

    Get current call duration.

    :returns: Call duration
    :rtype: Duration

.. dart:method:: Stream<Map<String, dynamic>>? get callStatsStream

    Stream of call statistics.

    :returns: Stats stream or null
    :rtype: Stream<Map<String, dynamic>>?

.. dart:method:: WebRTCService? get webrtcService

    Get WebRTC service instance for UI integration.

    :returns: WebRTC service or null
    :rtype: WebRTCService?

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
