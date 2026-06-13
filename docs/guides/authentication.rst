Authentication Guide
====================

This guide covers authentication and token management across all Nexacon SDKs.

Overview
--------

Nexacon uses token-based authentication to secure API requests. The authentication flow involves:

1. Obtain NX token from your Nexacon dashboard
2. Set the NX token for API requests
3. Token usage for API requests
4. Token refresh when expired
5. Logout and token invalidation

Authentication Flow
-------------------

**Setting the NX Token**

The NX token is obtained from your Nexacon dashboard and used to authenticate API requests:

.. tabs::

   .. code-tab:: flutter

      final client = NexaconClient(
        apiKey: 'your_api_key',
        secretKey: 'your_secret_key',
      );

      // Set the NX token
      client.setToken('your_nx_token');

   .. code-tab:: javascript

      const client = new NexaconClient({
        apiKey: 'your_api_key',
        secretKey: 'your_secret_key',
      });

      // Set the NX token
      client.setToken('your_nx_token');

   .. code-tab:: python

      client = NexaconClient(
          api_key='your_api_key',
          secret_key='your_secret_key'
      )

      # Set the NX token
      client.set_token('your_nx_token')

**Generating XMPP Token for Real-Time Features**

For real-time features like messaging and calls, you need to generate an XMPP token:

.. tabs::

   .. code-tab:: flutter

      final nxResponse = await client.auth.generateXMPPToken(
        username: '+255788811191',
      );

      final callManager = await client.createCallManager(
        nxtoken: nxResponse['token'],
        nxid: nxResponse['jid'],
        wsUrl: nxResponse['nxws'],
      );

   .. code-tab:: javascript

      const nxResponse = await client.auth.generateXMPPToken({
        username: '+255788811191',
      });

      const callManager = await client.createCallManager({
        nxtoken: nxResponse.token,
        nxid: nxResponse.jid,
        wsUrl: nxResponse.nxws,
      });

   .. code-tab:: python

      nx_response = client.auth.generate_xmpp_token(
          username='+255788811191'
      )

      call_manager = client.create_call_manager(
          nxtoken=nx_response['token'],
          nxid=nx_response['jid'],
          ws_url=nx_response['nxws']
      )

**Response**

The XMPP token response includes:

* **token**: XMPP token for real-time features
* **jid**: Jabber ID (JID) for the user
* **nxws**: WebSocket URL for real-time connections

Token Management
----------------

**Getting the Current Token**

Retrieve the currently set token:

.. tabs::

   .. code-tab:: flutter

      final token = client.getToken();

   .. code-tab:: javascript

      const token = client.getToken();

   .. code-tab:: python

      token = client.get_token()

**Clearing the Token**

Clear the token when logging out:

.. tabs::

   .. code-tab:: flutter

      client.setToken(null);

   .. code-tab:: javascript

      client.setToken(null);

   .. code-tab:: python

      client.set_token(None)

Best Practices
--------------

**Token Storage**

* **Mobile**: Use secure storage (Keychain on iOS, Keystore on Android)
* **Web**: Use httpOnly cookies or secure localStorage
* **Server**: Use environment variables or secure vaults

**Token Rotation**

* Implement automatic token rotation before expiration
* Handle token expiration gracefully
* Regenerate XMPP tokens for real-time features when needed

**Security**

* Never log tokens or include them in error messages
* Use HTTPS for all API requests
* Validate tokens on the server-side
* Implement token revocation for compromised accounts

Error Handling
-------------

**Invalid Token**

.. code-block:: text

    Error: Invalid token
    Solution: Verify the NX token is correct and not expired

**Expired Token**

.. code-block:: text

    Error: Token expired
    Solution: Generate a new NX token from your dashboard

**Missing Token**

.. code-block:: text

    Error: Token not set
    Solution: Set the NX token using setToken()

Example Implementation
----------------------

**Flutter**

.. code-block:: dart

    class AuthService {
      final NexaconClient _client;

      AuthService(this._client);

      Future<void> setToken(String nxToken) async {
        await _secureStorage.write(
          key: 'nx_token',
          value: nxToken,
        );

        _client.setToken(nxToken);
      }

      Future<String?> getToken() async {
        return await _secureStorage.read(key: 'nx_token');
      }

      Future<void> generateXMPPToken(String username) async {
        final nxResponse = await _client.auth.generateXMPPToken(
          username: username,
        );

        await _secureStorage.write(
          key: 'xmpp_token',
          value: nxResponse['token'],
        );
        await _secureStorage.write(
          key: 'jid',
          value: nxResponse['jid'],
        );
        await _secureStorage.write(
          key: 'nxws',
          value: nxResponse['nxws'],
        );

        return nxResponse['token'];
      }

      Future<void> logout() async {
        _client.setToken(null);
        await _secureStorage.delete(key: 'nx_token');
        await _secureStorage.delete(key: 'xmpp_token');
        await _secureStorage.delete(key: 'jid');
        await _secureStorage.delete(key: 'nxws');
      }
    }

Next Steps
----------

* `Error Handling <error-handling.html>`_ - Learn about error handling
* `Best Practices <best-practices.html>`_ - Follow recommended practices
