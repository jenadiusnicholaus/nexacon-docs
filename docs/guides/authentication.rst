Authentication Guide
====================

This guide covers authentication and token management across all Nexacon SDKs.

Overview
--------

Nexacon uses API key and secret key authentication for API requests. For real-time features like calls, an NX token is generated using the username.

Authentication Flow
-------------------

**Client Initialization**

Initialize the client with your API credentials:

.. tabs::

   .. code-tab:: flutter

      final client = NexaconClient(
        apiKey: 'your_api_key',
        secretKey: 'your_secret_key',
      );

   .. code-tab:: javascript

      const client = new NexaconClient({
        apiKey: 'your_api_key',
        secretKey: 'your_secret_key',
      });

   .. code-tab:: python

      client = NexaconClient(
          api_key='your_api_key',
          secret_key='your_secret_key'
      )

**Generating NX Token for Real-Time Features**

For real-time features like calls, generate an NX token using only the username:

.. tabs::

   .. code-tab:: flutter

      final nxResponse = await client.auth.generateNxToken(
        username: '+255788811191',
      );

      final callManager = await client.createCallManager(
        nxtoken: nxResponse['token'],
        nxid: nxResponse['nxid'],
        wsUrl: nxResponse['nxws'],
      );

   .. code-tab:: javascript

      const nxResponse = await client.auth.generateNxToken({
        username: '+255788811191',
      });

      const callManager = await client.createCallManager({
        nxtoken: nxResponse.token,
        nxid: nxResponse.nxid,
        wsUrl: nxResponse.nxws,
      });

   .. code-tab:: python

      nx_response = client.auth.generate_nx_token(
          username='+255788811191'
      )

      call_manager = client.create_call_manager(
          nxtoken=nx_response['token'],
          nxid=nx_response['nxid'],
          ws_url=nx_response['nxws']
      )

**Response**

The NX token response includes:

* **token**: NX token for real-time features
* **nxid**: Nexacon ID for the user
* **nxws**: WebSocket URL for real-time connections

Token Management
----------------

**Refreshing NX Token**

When the NX token expires, refresh it:

.. tabs::

   .. code-tab:: flutter

      final newToken = await client.auth.refreshNxToken(
        refreshToken: nxResponse['refresh_token'],
      );

   .. code-tab:: javascript

      const newToken = await client.auth.refreshNxToken({
        refreshToken: nxResponse.refresh_token,
      });

   .. code-tab:: python

      new_token = client.auth.refresh_nx_token(
          refresh_token=nx_response['refresh_token']
      )

Best Practices
--------------

**Token Storage**

* **Mobile**: Use secure storage (Keychain on iOS, Keystore on Android)
* **Web**: Use httpOnly cookies or secure localStorage
* **Server**: Use environment variables or secure vaults

**Token Rotation**

* Implement automatic token rotation before expiration
* Handle token expiration gracefully
* Regenerate NX tokens for real-time features when needed

**Security**

* Never log tokens or include them in error messages
* Use HTTPS for all API requests
* Validate tokens on the server-side
* Implement token revocation for compromised accounts

Error Handling
-------------

**Invalid Credentials**

.. code-block:: text

    Error: Invalid API key or secret key
    Solution: Verify your API credentials

**Invalid Username**

.. code-block:: text

    Error: Username is required
    Solution: Provide a valid username for NX token generation

**Expired Token**

.. code-block:: text

    Error: Token expired
    Solution: Refresh the NX token using refreshNxToken()

Example Implementation
----------------------

**Flutter**

.. code-block:: dart

    class AuthService {
      final NexaconClient _client;

      AuthService(this._client);

      Future<Map<String, dynamic>> generateNxToken(String username) async {
        final nxResponse = await _client.auth.generateNxToken(
          username: username,
        );

        await _secureStorage.write(
          key: 'nx_token',
          value: nxResponse['token'],
        );
        await _secureStorage.write(
          key: 'nx_id',
          value: nxResponse['nxid'],
        );
        await _secureStorage.write(
          key: 'nx_ws_url',
          value: nxResponse['nxws'],
        );

        return nxResponse;
      }

      Future<void> logout() async {
        await _secureStorage.delete(key: 'nx_token');
        await _secureStorage.delete(key: 'nx_id');
        await _secureStorage.delete(key: 'nx_ws_url');
      }
    }

Next Steps
----------

* `Error Handling <error-handling.html>`_ - Learn about error handling
* `Best Practices <best-practices.html>`_ - Follow recommended practices
