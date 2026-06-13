Getting Started
===============

This guide will help you get started with Nexacon SDKs. Choose your platform below to begin.

Choose Your Platform
--------------------

.. grid:: 2

   .. grid-item-card:: Flutter
      :columns: 3
      :link: flutter-sdk/index.html
      :link-type: doc

      Cross-platform mobile and desktop applications for Android, iOS, Linux, macOS, Web, and Windows.

   .. grid-item-card:: JavaScript
      :columns: 3
      :link: js-sdk/index.html
      :link-type: doc

      Browser and Node.js applications with full TypeScript support.

   .. grid-item-card:: React Native
      :columns: 3
      :link: react-native-sdk/index.html
      :link-type: doc

      iOS and Android mobile applications built with React Native.

   .. grid-item-card:: Python
      :columns: 3
      :link: python-sdk/index.html
      :link-type: doc

      Server-side and desktop applications with Python 3.7+.

   .. grid-item-card:: Java
      :columns: 3
      :link: java-sdk/index.html
      :link-type: doc

      Android and JVM applications with Java 8+.

   .. grid-item-card:: Go
      :columns: 3
      :link: go-sdk/index.html
      :link-type: doc

      Server-side and microservices with Go 1.16+.

   .. grid-item-card:: PHP
      :columns: 3
      :link: php-sdk/index.html
      :link-type: doc

      Web applications with PHP 7.4+.

   .. grid-item-card:: Ruby
      :columns: 3
      :link: ruby-sdk/index.html
      :link-type: doc

      Web applications with Ruby 2.7+.

   .. grid-item-card:: C#
      :columns: 3
      :link: csharp-sdk/index.html
      :link-type: doc

      .NET applications with C# 8.0+.

Prerequisites
-------------

Before using any Nexacon SDK, you will need:

* **Nexacon API Key** - Contact Nexacon to obtain your API key and secret
* **Development Environment** - Set up the development environment for your chosen platform
* **Account** - A Nexacon account for testing and development

First Steps
-----------

1. **Choose your SDK** - Select the SDK that matches your platform and language
2. **Install the SDK** - Follow the installation guide for your chosen SDK
3. **Initialize the client** - Set up the Nexacon client with your API credentials
4. **Authenticate** - Implement user authentication
5. **Build your first feature** - Start with messaging or calling

Common Concepts
---------------

All Nexacon SDKs share common concepts and patterns:

**Client Initialization**

Every SDK requires initializing a client with your API credentials:

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

**Authentication**

Authenticate users with their credentials:

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

**Sending Messages**

Send messages to other users:

.. tabs::

   .. code-tab:: flutter

      await client.messaging.send(
        to: '+255788811191',
        message: 'Hello!',
      );

   .. code-tab:: javascript

      await client.messaging.send({
        to: '+255788811191',
        message: 'Hello!',
      });

   .. code-tab:: python

      client.messaging.send(
          to='+255788811191',
          message='Hello!'
      )

Next Steps
----------

* `Installation Guide <installation.html>`_ - Detailed installation instructions
* `Authentication Guide <guides/authentication.html>`_ - Learn about authentication
* `API Reference` - Explore the API for your chosen SDK
* `Best Practices <guides/best-practices.html>`_ - Follow recommended practices
