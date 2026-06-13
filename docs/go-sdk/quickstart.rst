Go SDK Quick Start
=================

Get up and running with the Nexacon Go SDK in minutes.

Initialize the Client
---------------------

.. code-block:: go

    package main

    import "github.com/nexacon/nexacon-go-sdk"

    func main() {
        client := nexacon.NewClient("your_api_key", "your_secret_key")
    }

Available Services
------------------

Once the client is initialized, all services are available:

.. code-block:: go

    client.Auth        // Authentication and token management
    client.Messaging   // Send messages and manage contacts
    client.Calls       // Audio/video calls
    client.Devices     // Device registration for push notifications
    client.Rooms       // Group chat rooms
    client.Presence    // User presence and online status

Authentication
--------------

.. code-block:: go

    // Generate XMPP token for real-time features
    nxResponse, err := client.Auth.GenerateXMPPToken("+255788811191")
    if err != nil {
        log.Fatal(err)
    }

    fmt.Println("XMPP token:", nxResponse.Token)
    fmt.Println("JID:", nxResponse.JID)
    fmt.Println("WebSocket URL:", nxResponse.Nxws)

Messaging
---------

.. code-block:: go

    // Send a message
    err := client.Messaging.Send("+255788811191", "Hello!")
    if err != nil {
        log.Fatal(err)
    }

    // Get message history
    messages, err := client.Messaging.GetHistory("+255788811191", 1, 50)
    if err != nil {
        log.Fatal(err)
    }

    fmt.Println("Messages:", messages.Messages)

Calls
-----

.. code-block:: go

    // Initiate a video call
    call, err := client.Calls.InitiateCall("+255788811191", "video", "my-room")
    if err != nil {
        log.Fatal(err)
    }

    fmt.Println("Call ID:", call.CallID)

    // End the call
    err = client.Calls.EndCall(call.CallID)
    if err != nil {
        log.Fatal(err)
    }

Device Registration
-------------------

.. code-block:: go

    // Register device for push notifications
    err := client.Devices.Register("device_fcm_token", "android")
    if err != nil {
        log.Fatal(err)
    }

Presence
--------

.. code-block:: go

    // Get user presence
    presence, err := client.Presence.GetStatus("+255788811191")
    if err != nil {
        log.Fatal(err)
    }

    fmt.Println("Online:", presence.Online)

    // Get last seen
    lastSeen, err := client.Presence.GetLastSeen("+255788811191")
    if err != nil {
        log.Fatal(err)
    }

    fmt.Println("Last seen:", lastSeen.Timestamp)

Complete Example
----------------

.. code-block:: go

    package main

    import (
        "fmt"
        "log"
        "github.com/nexacon/nexacon-go-sdk"
    )

    func main() {
        // Initialize client
        client := nexacon.NewClient("your_api_key", "your_secret_key")

        // Generate XMPP token for real-time features
        nxResponse, err := client.Auth.GenerateXMPPToken("+255788811191")
        if err != nil {
            log.Fatal(err)
        }

        // Send message
        err = client.Messaging.Send("+255788811191", "Hello from Go!")
        if err != nil {
            log.Fatal(err)
        }

        // Make a call
        call, err := client.Calls.InitiateCall("+255788811191", "video", "my-room")
        if err != nil {
            log.Fatal(err)
        }

        fmt.Println("Call initiated:", call.CallID)
    }

Next Steps
----------

* `API Reference <api-reference.html>`_ - Detailed API documentation
* `Messaging <messaging.html>`_ - Messaging features
* `Calls <calls.html>`_ - Calling features
* `Best Practices <../guides/best-practices.html>`_ - Recommended practices
