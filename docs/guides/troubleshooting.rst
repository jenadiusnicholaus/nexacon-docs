Troubleshooting
===============

This guide covers common issues and their solutions across all Nexacon SDKs.

Common Issues
-------------

**Authentication Issues**

Problem: Login fails with "Invalid credentials"

Solution:
- Verify username and password are correct
- Check that the account is active
- Ensure API credentials are valid

Problem: Token expired error

Solution:
- Implement automatic token refresh
- Check token expiration time
- Re-authenticate if refresh token is also expired

**Network Issues**

Problem: Network connection failed

Solution:
- Check internet connection
- Verify API endpoint is accessible
- Check firewall settings
- Ensure HTTPS is allowed

Problem: Request timeout

Solution:
- Increase timeout duration
- Check network latency
- Implement retry logic with exponential backoff

**Platform-Specific Issues**

Flutter
^^^^^^^

Problem: Build fails on iOS

Solution:
- Run `flutter doctor` to check environment
- Update Xcode to latest version
- Clean build: `flutter clean && flutter pub get`
- Reinstall pods: `cd ios && pod install`

Problem: Build fails on Android

Solution:
- Update Android SDK
- Check `minSdkVersion` in build.gradle
- Clean build: `flutter clean && flutter pub get`
- Rebuild: `flutter build apk --debug`

JavaScript
^^^^^^^^^

Problem: Module not found

Solution:
- Ensure SDK is installed: `npm install nexacon-sdk`
- Check import path is correct
- Verify package.json dependencies

Problem: CORS error in browser

Solution:
- Configure CORS on server
- Use proxy for development
- Ensure API endpoint allows your domain

React Native
^^^^^^^^^^^^

Problem: iOS build fails

Solution:
- Update pods: `cd ios && pod install`
- Clean build: `npx react-native start --reset-cache`
- Check iOS deployment target

Problem: Android build fails

Solution:
- Clean gradle: `cd android && ./gradlew clean`
- Update Android SDK
- Check `minSdkVersion`

Python
^^^^^^

Problem: Import error

Solution:
- Ensure SDK is installed: `pip install nexacon-sdk`
- Check Python version (>= 3.7)
- Use virtual environment

Problem: SSL certificate error

Solution:
- Update certificates
- Use `pip install --upgrade certifi`
- Check system time

Java
^^^^

Problem: Dependency resolution error

Solution:
- Update Maven/Gradle
- Clear cache: `mvn dependency:purge-local-repository`
- Check repository configuration

Problem: Class not found

Solution:
- Verify dependency is added
- Clean and rebuild project
- Check classpath

Go
^^

Problem: Module not found

Solution:
- Run `go mod tidy`
- Check go.mod file
- Verify import path

PHP
^^^

Problem: Autoload error

Solution:
- Run `composer dump-autoload`
- Check composer.json
- Verify vendor directory

Ruby
^^^^

Problem: Gem not found

Solution:
- Run `bundle install`
- Check Gemfile
- Update Ruby version

C#
^^

Problem: Package not found

Solution:
- Run `dotnet restore`
- Check .csproj file
- Update NuGet packages

Debugging Tips
-------------

**Enable Debug Logging**

Flutter
^^^^^^^

.. code-block:: dart

    import 'package:flutter/foundation.dart';

    void main() {
      FlutterError.onError = (details) {
        FlutterError.dumpErrorToConsole(details);
      };
      runApp(MyApp());
    }

JavaScript
^^^^^^^^^

.. code-block:: javascript

    // Enable debug mode
    const client = new NexaconClient({
      apiKey: 'your_api_key',
      secretKey: 'your_secret_key',
      debug: true,
    });

Python
^^^^^^

.. code-block:: python

    import logging

    logging.basicConfig(level=logging.DEBUG)
    logger = logging.getLogger('nexacon')

**Check Network Requests**

Use network monitoring tools:

* **Browser**: DevTools Network tab
* **Flutter**: Flutter DevTools Network view
* **Node.js**: Wireshark or Charles Proxy
* **Mobile**: Charles Proxy or mitmproxy

**Validate API Responses**

Check API response structure:

.. code-block:: javascript

    try {
      const response = await client.auth.login({ username, password });
      console.log('Response:', JSON.stringify(response, null, 2));
    } catch (error) {
      console.error('Error:', error);
      console.error('Response:', error.response);
    }

Getting Help
------------

**Check Documentation**

* Review SDK-specific documentation
* Check API reference
* Read guides and best practices

**Search Issues**

* Check GitHub issues for similar problems
* Search Stack Overflow
* Review community forums

**Contact Support**

If you can't resolve the issue:

1. Gather information:
   - SDK version
   - Platform and version
   - Error message and stack trace
   - Steps to reproduce
   - Code snippet

2. Create a support request:
   - Email: support@nexacon.com
   - GitHub: https://github.com/nexacon/nexacon-docs/issues
   - Include all gathered information

**Provide Minimal Reproduction**

When reporting issues, provide a minimal reproduction:

.. code-block:: dart

    // Minimal reproduction example
    import 'package:nexacon_sdk/nexacon_sdk.dart';

    void main() async {
      final client = NexaconClient(
        apiKey: 'your_api_key',
        secretKey: 'your_secret_key',
      );

      try {
        final token = await client.auth.login(
          username: 'test@example.com',
          password: 'password',
        );
        print('Success: $token');
      } catch (e) {
        print('Error: $e');
      }
    }

Performance Issues
------------------

**Slow API Responses**

Solution:
- Check network latency
- Implement caching
- Use batch operations
- Optimize query parameters

**High Memory Usage**

Solution:
- Implement proper cleanup
- Use object pooling
- Limit concurrent requests
- Monitor memory usage

**Battery Drain (Mobile)**

Solution:
- Optimize polling intervals
- Use push notifications instead of polling
- Implement proper lifecycle management
- Background task optimization

Security Issues
---------------

**Token Theft**

Solution:
- Use secure storage
- Implement token encryption
- Shorten token expiration
- Monitor for suspicious activity

**Man-in-the-Middle Attacks**

Solution:
- Always use HTTPS
- Implement certificate pinning
- Validate SSL certificates
- Use secure APIs only

**Data Leakage**

Solution:
- Encrypt sensitive data
- Implement proper logging (no sensitive data)
- Use secure communication channels
- Regular security audits

Next Steps
----------

* `Authentication Guide <authentication.html>`_ - Learn about authentication
* `Error Handling <error-handling.html>`_ - Handle errors effectively
* `Best Practices <best-practices.html>`_ - Follow recommended practices
