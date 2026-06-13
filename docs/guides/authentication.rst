Authentication Guide
====================

This guide covers authentication and token management across all Nexacon SDKs.

Overview
--------

Nexacon uses token-based authentication to secure API requests. The authentication flow involves:

1. User login with credentials
2. Token generation (access token + refresh token)
3. Token usage for API requests
4. Token refresh when expired
5. Logout and token invalidation

Login Flow
-----------

**Basic Login**

.. tabs::

   .. code-tab:: flutter

      final token = await client.auth.login(
        username: 'user@example.com',
        password: 'password',
      );

   .. code-tab:: javascript

      const token = await client.auth.login({
        username: 'user@example.com',
        password: 'password',
      });

   .. code-tab:: python

      token = client.auth.login(
          username='user@example.com',
          password='password'
      )

**Response**

The login response includes:

* **access_token**: Short-lived token for API requests (typically 1 hour)
* **refresh_token**: Long-lived token for refreshing access tokens (typically 30 days)
* **expires_in**: Time until access token expires (in seconds)
* **token_type**: Token type (usually "Bearer")

Token Management
----------------

**Setting the Token**

After login, set the access token for subsequent API requests:

.. tabs::

   .. code-tab:: flutter

      client.setToken(token['access_token']);

   .. code-tab:: javascript

      client.setToken(token.access_token);

   .. code-tab:: python

      client.set_token(token['access_token'])

**Refreshing the Token**

When the access token expires, use the refresh token to obtain a new one:

.. tabs::

   .. code-tab:: flutter

      final newToken = await client.auth.refreshToken(
        refreshToken: token['refresh_token'],
      );
      client.setToken(newToken['access_token']);

   .. code-tab:: javascript

      const newToken = await client.auth.refreshToken(token.refresh_token);
      client.setToken(newToken.access_token);

   .. code-tab:: python

      new_token = client.auth.refresh_token(token['refresh_token'])
      client.set_token(new_token['access_token'])

**Logout**

Logout the user and invalidate the token:

.. tabs::

   .. code-tab:: flutter

      await client.auth.logout();

   .. code-tab:: javascript

      await client.auth.logout();

   .. code-tab:: python

      client.auth.logout()

Best Practices
--------------

**Token Storage**

* **Mobile**: Use secure storage (Keychain on iOS, Keystore on Android)
* **Web**: Use httpOnly cookies or secure localStorage
* **Server**: Use environment variables or secure vaults

**Token Refresh**

* Implement automatic token refresh before expiration
* Handle refresh token expiration gracefully
* Prompt user to re-login if refresh fails

**Security**

* Never log tokens or include them in error messages
* Use HTTPS for all API requests
* Validate tokens on the server-side
* Implement token revocation for compromised accounts

Error Handling
-------------

**Invalid Credentials**

.. code-block:: text

    Error: Invalid username or password

**Expired Token**

.. code-block:: text

    Error: Token expired
    Solution: Refresh the token using the refresh token

**Invalid Token**

.. code-block:: text

    Error: Invalid token
    Solution: Re-authenticate the user

**Refresh Token Expired**

.. code-block:: text

    Error: Refresh token expired
    Solution: Prompt user to login again

Example Implementation
----------------------

**Flutter**

.. code-block:: dart

    class AuthService {
      final NexaconClient _client;

      AuthService(this._client);

      Future<void> login(String username, String password) async {
        final token = await _client.auth.login(
          username: username,
          password: password,
        );

        await _secureStorage.write(
          key: 'access_token',
          value: token['access_token'],
        );
        await _secureStorage.write(
          key: 'refresh_token',
          value: token['refresh_token'],
        );

        _client.setToken(token['access_token']);
      }

      Future<void> refreshToken() async {
        final refreshToken = await _secureStorage.read(
          key: 'refresh_token',
        );

        if (refreshToken == null) {
          throw Exception('No refresh token available');
        }

        final newToken = await _client.auth.refreshToken(
          refreshToken: refreshToken,
        );

        await _secureStorage.write(
          key: 'access_token',
          value: newToken['access_token'],
        );

        _client.setToken(newToken['access_token']);
      }

      Future<void> logout() async {
        await _client.auth.logout();
        await _secureStorage.delete(key: 'access_token');
        await _secureStorage.delete(key: 'refresh_token');
      }
    }

Next Steps
----------

* `Error Handling <error-handling.html>`_ - Learn about error handling
* `Best Practices <best-practices.html>`_ - Follow recommended practices
