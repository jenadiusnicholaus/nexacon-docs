Best Practices
==============

This guide covers recommended practices for using Nexacon SDKs effectively.

General Best Practices
---------------------

**Secure Credential Management**

* Never hardcode API keys or secrets in your code
* Use environment variables or secure vaults
* Rotate credentials regularly
* Use different credentials for development and production

**Token Management**

* Store tokens securely (Keychain, Keystore, secure storage)
* Implement automatic token refresh
* Handle token expiration gracefully
* Invalidate tokens on logout

**Error Handling**

* Always implement error handling
* Log errors with context
* Provide user-friendly error messages
* Implement retry logic for transient errors

**Network Optimization**

* Implement request caching where appropriate
* Use connection pooling
* Implement exponential backoff for retries
* Monitor network performance

**Security**

* Always use HTTPS
* Validate all user inputs
* Implement rate limiting
* Keep SDKs updated

Platform-Specific Best Practices
---------------------------------

**Flutter**

.. code-block:: dart

    // Use secure storage for tokens
    final secureStorage = FlutterSecureStorage();

    // Implement proper state management
    class AuthProvider extends ChangeNotifier {
      NexaconClient? _client;

      Future<void> login(String username, String password) async {
        _client = NexaconClient(
          apiKey: apiKey,
          secretKey: secretKey,
        );

        final token = await _client!.auth.login(
          username: username,
          password: password,
        );

        await secureStorage.write(
          key: 'access_token',
          value: token['access_token'],
        );

        _client!.setToken(token['access_token']);
        notifyListeners();
      }
    }

**JavaScript**

.. code-block:: javascript

    // Use environment variables
    const client = new NexaconClient({
      apiKey: process.env.NEXACON_API_KEY,
      secretKey: process.env.NEXACON_SECRET_KEY,
    });

    // Implement request interceptors
    axios.interceptors.request.use(config => {
      const token = localStorage.getItem('access_token');
      if (token) {
        config.headers.Authorization = `Bearer ${token}`;
      }
      return config;
    });

**Python**

.. code-block:: python

    # Use environment variables
    import os
    from dotenv import load_dotenv

    load_dotenv()

    client = NexaconClient(
        api_key=os.getenv('NEXACON_API_KEY'),
        secret_key=os.getenv('NEXACON_SECRET_KEY')
    )

    # Use context managers for resources
    with NexaconClient(api_key, secret_key) as client:
        client.auth.login(username, password)

**React Native**

.. code-block:: typescript

    // Use AsyncStorage for token storage
    import AsyncStorage from '@react-native-async-storage/async-storage';

    const storeToken = async (token: string) => {
      await AsyncStorage.setItem('access_token', token);
    };

    // Implement proper cleanup
    useEffect(() => {
      return () => {
        client.dispose();
      };
    }, []);

Performance Optimization
------------------------

**Batch Operations**

Combine multiple operations when possible:

.. code-block:: dart

    // Bad: Multiple individual requests
    for (var user in users) {
      await client.presence.getStatus(user.id);
    }

    // Good: Batch request
    final statuses = await client.presence.getBatchStatus(
      users.map((u) => u.id).toList(),
    );

**Caching**

Implement caching for frequently accessed data:

.. code-block:: javascript

    class Cache {
      constructor(ttl = 60000) {
        this.cache = new Map();
        this.ttl = ttl;
      }

      get(key) {
        const item = this.cache.get(key);
        if (item && Date.now() - item.timestamp < this.ttl) {
          return item.data;
        }
        this.cache.delete(key);
        return null;
      }

      set(key, data) {
        this.cache.set(key, { data, timestamp: Date.now() });
      }
    }

**Lazy Loading**

Load resources only when needed:

.. code-block:: dart

    class LazyLoader {
      NexaconClient? _client;

      NexaconClient get client {
        _client ??= NexaconClient(
          apiKey: apiKey,
          secretKey: secretKey,
        );
        return _client!;
      }
    }

Testing
-------

**Unit Testing**

Write unit tests for your business logic:

.. code-block:: dart

    test('should login with valid credentials', () async {
      final client = MockNexaconClient();
      when(client.auth.login(
        username: 'test@example.com',
        password: 'password',
      )).thenAnswer((_) async => {'access_token': 'token'});

      final auth = AuthService(client);
      await auth.login('test@example.com', 'password');

      verify(client.auth.login(
        username: 'test@example.com',
        password: 'password',
      )).called(1);
    });

**Integration Testing**

Test integration with the actual API:

.. code-block:: python

    @pytest.mark.integration
    def test_login_integration():
        client = NexaconClient(
            api_key=os.getenv('TEST_API_KEY'),
            secret_key=os.getenv('TEST_SECRET_KEY')
        )
        token = client.auth.login(
            username='test@example.com',
            password='password'
        )
        assert 'access_token' in token

**Mock API Responses**

Mock API responses for development:

.. code-block:: javascript

    const mockClient = {
      auth: {
        login: jest.fn().mockResolvedValue({
          access_token: 'mock_token',
          refresh_token: 'mock_refresh_token',
        }),
      },
    };

Monitoring
-----------

**Logging**

Implement structured logging:

.. code-block:: python

    import logging

    logger = logging.getLogger('nexacon')
    logger.setLevel(logging.INFO)

    handler = logging.StreamHandler()
    handler.setFormatter(logging.Formatter(
        '%(asctime)s - %(name)s - %(levelname)s - %(message)s'
    ))
    logger.addHandler(handler)

**Metrics**

Track key metrics:

* API request latency
* Error rates
* Token refresh frequency
* Network usage

**Alerting**

Set up alerts for critical issues:

* High error rates
* Authentication failures
* API downtime

Code Organization
-----------------

**Separation of Concerns**

Separate business logic from SDK usage:

.. code-block:: dart

    // Service layer
    class MessagingService {
      final NexaconClient _client;

      Future<void> sendMessage(String to, String message) async {
        await _client.messaging.send(to: to, message: message);
      }
    }

    // UI layer
    class MessagingWidget extends StatelessWidget {
      final MessagingService _service;

      Future<void> _handleSend() async {
        await _service.sendMessage(recipient, message);
      }
    }

**Dependency Injection**

Use dependency injection for testability:

.. code-block:: typescript

    interface IMessagingService {
      send(to: string, message: string): Promise<void>;
    }

    class MessagingService implements IMessagingService {
      constructor(private client: NexaconClient) {}

      async send(to: string, message: string) {
        await this.client.messaging.send({ to, message });
      }
    }

**Configuration Management**

Centralize configuration:

.. code-block:: javascript

    // config.js
    export const config = {
      api: {
        key: process.env.NEXACON_API_KEY,
        secret: process.env.NEXACON_SECRET_KEY,
        baseUrl: process.env.NEXACON_BASE_URL,
      },
      features: {
        messaging: true,
        calls: true,
      },
    };

Next Steps
----------

* `Authentication Guide <authentication.html>`_ - Learn about authentication
* `Error Handling <error-handling.html>`_ - Handle errors effectively
* `Troubleshooting <troubleshooting.html>`_ - Common issues and solutions
