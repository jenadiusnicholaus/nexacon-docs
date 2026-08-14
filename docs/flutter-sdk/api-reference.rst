Flutter SDK API Reference
=========================

This section provides detailed API reference for the Nexacon Flutter SDK.

NexaconSDK
----------

.. dart:class:: NexaconSDK

    Simplified high-level API for Nexacon SDK. Handles all complexity internally — just create an instance, set callbacks, and call ``startCall()``.

.. dart:method:: NexaconSDK({required String apiKey, required String secretKey, String baseUrl = 'your-domain.com/api/v1.0'})

    Create a NexaconSDK instance.

    :param apiKey: Your Nexacon API key
    :type apiKey: String
    :param secretKey: Your Nexacon secret key
    :type secretKey: String
    :param baseUrl: Base URL for API requests (optional)
    :type baseUrl: String

**Callbacks**

All callbacks are optional. Set them before making or receiving calls.

.. dart:method:: Function(CallState)? onCallStateChanged

    Called when the call state changes (idle, calling, incoming, connected, ended).

.. dart:method:: Function(String)? onIncomingCall

    Called when an incoming call is received. Parameter is the caller's display name.

.. dart:method:: Function(String)? onCallEnded

    Called when a call ends. Parameter is the reason string.

.. dart:method:: Function(String)? onError

    Called when an error occurs. Parameter is the error message.

.. dart:method:: Function()? onLocalStream

    Called when the local media stream is ready.

.. dart:method:: Function()? onRemoteStream

    Called when the remote media stream is ready.

.. dart:method:: Function()? onOtherUserJoined

    Called when the remote peer joins the call.

.. dart:method:: Function()? onOtherUserLeft

    Called when the remote peer leaves the call.

**Methods**

.. dart:method:: Future<Map<String, dynamic>> initialize({required String username, String? name, String? nxtoken, String? nxid, String? wsUrl})

    Initialize the SDK connection without starting a call. Use this for pre-warming (incoming calls) or before ``startCall()``.

    :param username: Your username or phone number
    :type username: String
    :param name: Your display name (optional)
    :type name: String?
    :param nxtoken: Pre-fetched NX token (optional, skips API call)
    :type nxtoken: String?
    :param nxid: Pre-fetched NX ID (optional)
    :type nxid: String?
    :param wsUrl: Pre-fetched WebSocket URL (optional)
    :type wsUrl: String?
    :returns: NX credentials used (token, nxid, nxws)
    :rtype: Future<Map<String, dynamic>>

.. dart:method:: Future<void> startCall({required String to, required String username, String? name, bool audio = true, bool video = false, String? roomId})

    Start an outgoing call. Handles everything internally: fetches NX token, connects, and initiates the call. Reuses pre-warmed connection if available.

    :param to: Recipient's phone number
    :type to: String
    :param username: Your username or phone number
    :type username: String
    :param name: Your display name (optional)
    :type name: String?
    :param audio: Enable audio (default: true)
    :type audio: bool
    :param video: Enable video (default: false)
    :type video: bool
    :param roomId: Custom room ID (auto-generated if omitted)
    :type roomId: String?

.. dart:method:: Future<void> acceptCall({bool audio = true, bool video = false})

    Accept an incoming call. Must be called after ``onIncomingCall`` has fired.

    :param audio: Enable audio (default: true)
    :type audio: bool
    :param video: Enable video (default: false)
    :type video: bool

.. dart:method:: Future<void> acceptWhenReady({required String username, String? name, bool audio = true, bool video = false, Duration timeout = const Duration(seconds: 30)})

    Initialize and automatically accept the incoming call once the call invitation signal arrives. This is the recommended way to handle incoming calls when the app is already in the foreground.

    :param username: Your username or phone number
    :type username: String
    :param name: Your display name (optional)
    :type name: String?
    :param audio: Enable audio (default: true)
    :type audio: bool
    :param video: Enable video (default: false)
    :type video: bool
    :param timeout: How long to wait for the call invitation (default: 30s)
    :type timeout: Duration

.. dart:method:: Future<void> acceptFromNotification({required String username, required String roomId, required String callerNxId, String? callerName, String? name, bool audio = true, bool video = false})

    Accept an incoming call using data from a push notification payload. Use this when FCM already delivered the call data so you don't need to wait for the signaling invitation.

    :param username: Your username or phone number
    :type username: String
    :param roomId: Room ID from the FCM push payload
    :type roomId: String
    :param callerNxId: Caller's NX ID from the FCM push payload
    :type callerNxId: String
    :param callerName: Caller's display name (optional)
    :type callerName: String?
    :param name: Your display name (optional)
    :type name: String?
    :param audio: Enable audio (default: true)
    :type audio: bool
    :param video: Enable video (default: false)
    :type video: bool

.. dart:method:: void rejectCall()

    Reject an incoming call.

.. dart:method:: void notifyRemoteAccepted()

    Notify the SDK that the remote party accepted the call (FCM/backend fallback).

.. dart:method:: Future<void> endCall()

    End the current call. Nulls out the internal CallManager so the next call gets a fresh instance.

.. dart:method:: void toggleMute(bool muted)

    Mute or unmute the microphone.

    :param muted: ``true`` to mute, ``false`` to unmute
    :type muted: bool

.. dart:method:: void toggleSpeaker(bool enabled)

    Enable or disable the speakerphone.

    :param enabled: ``true`` to enable speaker, ``false`` to disable
    :type enabled: bool

.. dart:method:: void toggleVideo(bool enabled)

    Enable or disable the camera.

    :param enabled: ``true`` to enable camera, ``false`` to disable
    :type enabled: bool

.. dart:method:: Future<void> switchCamera()

    Switch between front and back camera.

.. dart:method:: Duration get callDuration

    Get the current call duration.

    :returns: Call duration
    :rtype: Duration

.. dart:method:: NexaconClient? get client

    Get the underlying NexaconClient for advanced use cases (devices, rooms, presence).

    :returns: NexaconClient instance or null
    :rtype: NexaconClient?

.. dart:method:: Future<void> dispose()

    Clean up all resources (CallManager, client, NX connection). Call this when done with the SDK.

CallState Enum
^^^^^^^^^^^^^^

.. dart:enum:: CallState

    Enum representing call states.

    * ``CallState.idle`` - No active call
    * ``CallState.calling`` - Outgoing call in progress
    * ``CallState.incoming`` - Incoming call waiting to be accepted
    * ``CallState.connected`` - Call is connected
    * ``CallState.ended`` - Call has ended

NexaconClient (Advanced)
------------------------

.. dart:class:: NexaconClient

    Low-level client class for interacting with the Nexacon API. Access via ``sdk.client`` or create directly for advanced use cases.

.. dart:method:: NexaconClient({required String apiKey, required String secretKey, String? baseUrl})

    Initialize a new NexaconClient instance.

    :param apiKey: API key for authentication
    :type apiKey: String
    :param secretKey: Secret key for authentication
    :type secretKey: String
    :param baseUrl: Base URL for API requests (default: your-domain.com/api/v1.0)
    :type baseUrl: String?

.. dart:method:: Future<Map<String, dynamic>> auth.getNxToken({required String username})

    Get NX token for real-time features (calls and signaling).

    :param username: User's username or phone number
    :type username: String
    :returns: NX token response containing ``token``, ``nxid``, and ``nxws``
    :rtype: Future<Map<String, dynamic>>

.. dart:method:: Future<Map<String, dynamic>> auth.refreshNxToken({required String refreshToken})

    Refresh an expired NX token.

    :param refreshToken: Refresh token from previous auth response
    :type refreshToken: String
    :returns: New NX token response
    :rtype: Future<Map<String, dynamic>>

.. dart:method:: Future<CallManager> createCallManager({String? nxtoken, String? nxid, String? wsUrl, String? name, Function(CallState)? onCallStateChanged, Function(String)? onIncomingCall, Function(String)? onCallEnded, Function(String)? onError, Function(MediaStream)? onLocalStream, Function(MediaStream)? onRemoteStream, Function()? onOtherUserJoined, Function()? onOtherUserLeft})

    Create a call manager instance directly. Prefer using ``NexaconSDK`` instead.

    :returns: CallManager instance
    :rtype: Future<CallManager>

CallManager (Advanced)
----------------------

.. dart:class:: CallManager

    Low-level calling service for P2P audio/video calls using WebRTC. Access via ``sdk.client?.createCallManager()`` or use ``NexaconSDK`` which wraps this internally.

.. dart:method:: Future<bool> initialize({required String nxid, required String nxtoken, required String wsUrl, String? name})

    Initialize the call manager with NX credentials.

.. dart:method:: Future<void> initiateCall({required String to, bool audio = true, bool video = true, String? roomId})

    Initiate an outgoing P2P call.

.. dart:method:: void prepareIncomingCall({required String roomId, required String callerNxId, String callerName = 'Unknown'})

    Inject incoming call state from push notification data.

.. dart:method:: Future<void> acceptCall({bool audio = true, bool video = true})

    Accept an incoming call.

.. dart:method:: void rejectCall()

    Reject an incoming call.

.. dart:method:: void notifyRemoteAccepted()

    Notify that the remote party accepted (FCM fallback).

.. dart:method:: Future<void> endCall()

    End the current call.

.. dart:method:: void toggleAudio(bool enabled)

    Enable/disable audio.

.. dart:method:: void toggleVideo(bool enabled)

    Enable/disable video.

.. dart:method:: Future<void> switchCamera()

    Switch between front and back camera.

.. dart:method:: void setVideoQuality({int width = 1280, int height = 720, int fps = 30})

    Set video resolution and frame rate.

.. dart:method:: void setAudioBitrate(int kbps)

    Set audio bitrate.

.. dart:method:: void setVideoBitrate(int kbps)

    Set video bitrate.

.. dart:method:: void startCallStatsCollection({Duration interval = const Duration(seconds: 2)})

    Start collecting WebRTC call statistics.

.. dart:method:: CallState get callState

    Get current call state.

.. dart:method:: Duration get callDuration

    Get current call duration.

.. dart:method:: Stream<Map<String, dynamic>>? get callStatsStream

    Stream of call statistics.

.. dart:method:: WebRTCService? get webrtcService

    Get WebRTC service instance for UI integration.

.. note::
   **Real-Time Messaging**: For chat messaging (text messages, typing indicators, read receipts, presence, message history), use the separate `Nexacon Messaging SDK <https://nexacon-messaging.readthedocs.io/>`_.

Devices
-------

.. dart:method:: Future<void> devices.register({required String fcmToken, required String platform, String? deviceId})

    Register a device for push notifications.

    :param fcmToken: FCM token for the device
    :type fcmToken: String
    :param platform: Platform ('android' or 'ios')
    :type platform: String
    :param deviceId: Unique device identifier
    :type deviceId: String?

.. dart:method:: Future<void> devices.unregister(String fcmToken)

    Unregister a device from push notifications.

Rooms
-----

.. dart:method:: Future<Map<String, dynamic>> rooms.create({required String name, String? description, required List<String> members})

    Create a new group call room.

.. dart:method:: Future<Map<String, dynamic>> rooms.list({int page = 1, int pageSize = 50})

    List available rooms.

Presence
--------

.. dart:method:: Future<Map<String, dynamic>> presence.getStatus(String userId)

    Get the presence status of a user.

.. dart:method:: Future<Map<String, dynamic>> presence.getLastSeen(String userId)

    Get the last seen timestamp of a user.

FoldStateService
----------------

.. dart:class:: FoldStateService

    Service for detecting foldable device state changes.

.. dart:method:: Stream<FoldState> get foldStateStream

    Stream of fold state changes.

.. dart:method:: FoldState get currentState

    Get the current fold state.

.. dart:method:: bool get isFolded

    Check if device is folded.

.. dart:method:: bool get isFlat

    Check if device is flat.

.. dart:method:: bool get isHalfOpen

    Check if device is half-open.

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
