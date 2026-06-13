Java SDK Quick Start
===================

Get up and running with the Nexacon Java SDK in minutes.

Initialize the Client
---------------------

.. code-block:: java

    import com.nexacon.sdk.NexaconClient;

    NexaconClient client = new NexaconClient(
        "your_api_key",
        "your_secret_key"
    );

Available Services
------------------

Once the client is initialized, all services are available:

.. code-block:: java

    client.auth        // Authentication and token management
    client.messaging   // Send messages and manage contacts
    client.calls       // Audio/video calls
    client.devices     // Device registration for push notifications
    client.rooms       // Group chat rooms
    client.presence    // User presence and online status

Authentication
--------------

.. code-block:: java

    // Login user
    Map<String, Object> token = client.auth.login(
        "user@example.com",
        "password"
    );

    System.out.println("Access token: " + token.get("access_token"));
    System.out.println("Refresh token: " + token.get("refresh_token"));

    // Set token for subsequent requests
    client.setToken((String) token.get("access_token"));

Messaging
---------

.. code-block:: java

    // Send a message
    client.messaging.send(
        "+255788811191",
        "Hello!"
    );

    // Get message history
    Map<String, Object> messages = client.messaging.getHistory(
        "+255788811191",
        1,
        50
    );

    System.out.println("Messages: " + messages.get("messages"));

Calls
-----

.. code-block:: java

    // Initiate a video call
    Map<String, Object> call = client.calls.initiateCall(
        "+255788811191",
        "video",
        "my-room"
    );

    System.out.println("Call ID: " + call.get("call_id"));

    // End the call
    client.calls.endCall((String) call.get("call_id"));

Device Registration
-------------------

.. code-block:: java

    // Register device for push notifications
    client.devices.register(
        "device_fcm_token",
        "android"
    );

Presence
--------

.. code-block:: java

    // Get user presence
    Map<String, Object> presence = client.presence.getStatus("+255788811191");
    System.out.println("Online: " + presence.get("online"));

    // Get last seen
    Map<String, Object> lastSeen = client.presence.getLastSeen("+255788811191");
    System.out.println("Last seen: " + lastSeen.get("timestamp"));

Complete Example
----------------

.. code-block:: java

    import com.nexacon.sdk.NexaconClient;
import java.util.Map;

    public class Main {
        public static void main(String[] args) {
            // Initialize client
            NexaconClient client = new NexaconClient(
                "your_api_key",
                "your_secret_key"
            );

            // Authenticate
            Map<String, Object> token = client.auth.login(
                "user@example.com",
                "password"
            );

            client.setToken((String) token.get("access_token"));

            // Send message
            client.messaging.send(
                "+255788811191",
                "Hello from Java!"
            );

            // Make a call
            Map<String, Object> call = client.calls.initiateCall(
                "+255788811191",
                "video",
                "my-room"
            );

            System.out.println("Call initiated: " + call.get("call_id"));
        }
    }

Next Steps
----------

* `API Reference <api-reference.html>`_ - Detailed API documentation
* `Messaging <messaging.html>`_ - Messaging features
* `Calls <calls.html>`_ - Calling features
* `Best Practices <../guides/best-practices.html>`_ - Recommended practices
