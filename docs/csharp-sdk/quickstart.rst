C# SDK Quick Start
==================

Get up and running with the Nexacon C# SDK in minutes.

Initialize the Client
---------------------

.. code-block:: csharp

    using Nexacon.SDK;

    var client = new NexaconClient("your_api_key", "your_secret_key");

Available Services
------------------

Once the client is initialized, all services are available:

.. code-block:: csharp

    client.Auth        // Authentication and token management
    client.Messaging   // Send messages and manage contacts
    client.Calls       // Audio/video calls
    client.Devices     // Device registration for push notifications
    client.Rooms       // Group chat rooms
    client.Presence    // User presence and online status

Authentication
--------------

.. code-block:: csharp

    // Set the NX token (obtained from Nexacon dashboard)
    client.SetToken("your_nx_token");

    // Generate XMPP token for real-time features
    var nxResponse = await client.Auth.GenerateXMPPTokenAsync("+255788811191");

    Console.WriteLine($"XMPP token: {nxResponse.Token}");
    Console.WriteLine($"JID: {nxResponse.JID}");

Messaging
---------

.. code-block:: csharp

    // Send a message
    await client.Messaging.SendAsync("+255788811191", "Hello!");

    // Get message history
    var messages = await client.Messaging.GetHistoryAsync("+255788811191", 1, 50);

    Console.WriteLine($"Messages: {messages.Messages}");

Calls
-----

.. code-block:: csharp

    // Initiate a video call
    var call = await client.Calls.InitiateCallAsync("+255788811191", "video", "my-room");

    Console.WriteLine($"Call ID: {call.CallId}");

    // End the call
    await client.Calls.EndCallAsync(call.CallId);

Device Registration
-------------------

.. code-block:: csharp

    // Register device for push notifications
    await client.Devices.RegisterAsync("device_fcm_token", "android");

Presence
--------

.. code-block:: csharp

    // Get user presence
    var presence = await client.Presence.GetStatusAsync("+255788811191");
    Console.WriteLine($"Online: {presence.Online}");

    // Get last seen
    var lastSeen = await client.Presence.GetLastSeenAsync("+255788811191");
    Console.WriteLine($"Last seen: {lastSeen.Timestamp}");

Complete Example
----------------

.. code-block:: csharp

    using Nexacon.SDK;
    using System;
    using System.Threading.Tasks;

    class Program
    {
        static async Task Main(string[] args)
        {
            // Initialize client
            var client = new NexaconClient("your_api_key", "your_secret_key");

            // Set NX token (obtained from Nexacon dashboard)
            client.SetToken("your_nx_token");

            // Generate XMPP token for real-time features
            var nxResponse = await client.Auth.GenerateXMPPTokenAsync("+255788811191");

            // Send message
            await client.Messaging.SendAsync("+255788811191", "Hello from C#!");

            // Make a call
            var call = await client.Calls.InitiateCallAsync("+255788811191", "video", "my-room");

            Console.WriteLine($"Call initiated: {call.CallId}");
        }
    }

Next Steps
----------

* `API Reference <api-reference.html>`_ - Detailed API documentation
* `Messaging <messaging.html>`_ - Messaging features
* `Calls <calls.html>`_ - Calling features
* `Best Practices <../guides/best-practices.html>`_ - Recommended practices
