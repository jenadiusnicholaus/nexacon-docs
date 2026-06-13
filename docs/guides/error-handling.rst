Error Handling Guide
====================

This guide covers error handling across all Nexacon SDKs.

Overview
--------

All Nexacon SDKs follow consistent error handling patterns. Errors are typically raised as exceptions or returned in error responses.

Common Error Types
-----------------

**Authentication Errors**

* **InvalidCredentials**: Username or password is incorrect
* **TokenExpired**: Access token has expired
* **InvalidToken**: Token is invalid or malformed
* **RefreshTokenExpired**: Refresh token has expired

**Network Errors**

* **NetworkError**: Network connection failed
* **TimeoutError**: Request timed out
* **ServerError**: Server returned an error (5xx)
* **RateLimitError**: Too many requests

**Validation Errors**

* **ValidationError**: Invalid request parameters
* **MissingParameter**: Required parameter is missing
* **InvalidParameter**: Parameter value is invalid

**Resource Errors**

* **NotFoundError**: Resource not found
* **PermissionDenied**: Insufficient permissions
* **ConflictError**: Resource conflict

Error Handling Patterns
----------------------

**Flutter**

.. code-block:: dart

    try {
      final token = await client.auth.login(
        username: 'user@example.com',
        password: 'password',
      );
    } on InvalidCredentialsException {
      print('Invalid username or password');
    } on TokenExpiredException {
      print('Token expired, please refresh');
    } on NetworkException {
      print('Network error, please check your connection');
    } catch (e) {
      print('Unexpected error: $e');
    }

**JavaScript**

.. code-block:: javascript

    try {
      const token = await client.auth.login({
        username: 'user@example.com',
        password: 'password',
      });
    } catch (error) {
      if (error.code === 'INVALID_CREDENTIALS') {
        console.log('Invalid username or password');
      } else if (error.code === 'TOKEN_EXPIRED') {
        console.log('Token expired, please refresh');
      } else if (error.code === 'NETWORK_ERROR') {
        console.log('Network error, please check your connection');
      } else {
        console.log('Unexpected error:', error);
      }
    }

**Python**

.. code-block:: python

    try:
        token = client.auth.login(
            username='user@example.com',
            password='password'
        )
    except InvalidCredentialsError:
        print('Invalid username or password')
    except TokenExpiredError:
        print('Token expired, please refresh')
    except NetworkError:
        print('Network error, please check your connection')
    except Exception as e:
        print(f'Unexpected error: {e}')

Retry Logic
-----------

**Exponential Backoff**

Implement exponential backoff for retryable errors:

.. code-block:: python

    import time
    from nexacon_sdk import NetworkError

    def retry_with_backoff(func, max_retries=3):
        for attempt in range(max_retries):
            try:
                return func()
            except NetworkError:
                if attempt == max_retries - 1:
                    raise
                wait_time = 2 ** attempt
                time.sleep(wait_time)

**Retry on Specific Errors**

Only retry on retryable errors (network errors, rate limits):

.. code-block:: dart

    Future<T> retryWithBackoff<T>(
      Future<T> Function() fn, {
      int maxRetries = 3,
    }) async {
      for (int attempt = 0; attempt < maxRetries; attempt++) {
        try {
          return await fn();
        } on NetworkException catch (e) {
          if (attempt == maxRetries - 1) rethrow;
          await Future.delayed(Duration(seconds: 2 << attempt));
        }
      }
      throw Exception('Max retries exceeded');
    }

Error Logging
-------------

**Structured Logging**

Log errors with context for debugging:

.. code-block:: javascript

    function logError(error, context = {}) {
      console.error({
        timestamp: new Date().toISOString(),
        error: error.message,
        code: error.code,
        stack: error.stack,
        context: context,
      });
    }

    try {
      await client.auth.login({ username, password });
    } catch (error) {
      logError(error, { username, action: 'login' });
    }

**Error Tracking**

Integrate with error tracking services:

* **Sentry**: Capture and track errors
* **Rollbar**: Real-time error monitoring
* **Bugsnag**: Error and performance monitoring

User-Friendly Messages
----------------------

**Translate Technical Errors**

Convert technical error codes to user-friendly messages:

.. code-block:: dart

    String getErrorMessage(dynamic error) {
      if (error is InvalidCredentialsException) {
        return 'Invalid username or password';
      } else if (error is TokenExpiredException) {
        return 'Session expired, please login again';
      } else if (error is NetworkException) {
        return 'Network error, please check your connection';
      } else {
        return 'An unexpected error occurred';
      }
    }

**Actionable Messages**

Provide actionable error messages:

.. code-block:: text

    Bad: "Error 401"
    Good: "Your session has expired. Please login again."

    Bad: "Error 429"
    Good: "Too many requests. Please wait a moment and try again."

Best Practices
--------------

**Always Handle Errors**

Never ignore errors. Always implement error handling:

.. code-block:: dart

    // Bad
    await client.auth.login(username, password);

    // Good
    try {
      await client.auth.login(username, password);
    } catch (e) {
      handleError(e);
    }

**Log Errors**

Log errors for debugging and monitoring:

.. code-block:: python

    try:
        client.auth.login(username, password)
    except Exception as e:
        logger.error(f"Login failed: {e}", exc_info=True)

**Provide Context**

Include context when logging errors:

.. code-block:: javascript

    logger.error('Login failed', {
      error: error.message,
      username: username,
      timestamp: new Date().toISOString(),
    });

**Graceful Degradation**

Implement graceful degradation when possible:

.. code-block:: dart

    Future<List<Message>> getMessages() async {
      try {
        return await client.messaging.getHistory();
      } catch (e) {
        // Return cached messages on error
        return getCachedMessages();
      }
    }

Next Steps
----------

* `Authentication Guide <authentication.html>`_ - Learn about authentication
* `Best Practices <best-practices.html>`_ - Follow recommended practices
* `Troubleshooting <troubleshooting.html>`_ - Common issues and solutions
