Installation
============

This guide provides installation instructions for the Nexacon Flutter SDK.

Flutter SDK
-----------

**Requirements**

* Flutter SDK >= 3.0.0
* Dart SDK >= 3.0.0
* Platform-specific requirements:
  * Android: Android Studio and Android SDK
  * iOS: Xcode 14+ (macOS only)
  * Linux: GTK development libraries
  * macOS: Xcode command-line tools
  * Windows: Visual Studio 2022 with C++ workload
  * Web: Chrome or Edge browser

**Installation**

.. code-block:: bash

    flutter pub add nexacon_sdk

**Verification**

.. code-block:: dart

    import 'package:nexacon_sdk/nexacon_sdk.dart';

    void main() {
      print('Nexacon SDK installed successfully');
    }

.. note::
   For real-time chat messaging, install the separate Nexacon Messaging SDK:

   .. code-block:: bash

       flutter pub add nexacon_messaging

   See the `Nexacon Messaging SDK docs <https://nexacon-messaging.readthedocs.io/>`_ for more information.

API Credentials
---------------

After installing the SDK, you will need to configure it with your API credentials:

1. Sign up for a Nexacon account at https://nexacon.africa
2. Navigate to the Developer Portal
3. Create a new application
4. Copy your API Key and Secret Key

.. code-block:: text

    API Key: your_api_key_here
    Secret Key: your_secret_key_here

Troubleshooting
---------------

**Installation Fails**

* Ensure you have the required dependencies installed
* Check that your development environment is properly configured
* Try clearing your package manager cache

**Import Errors**

* Verify the SDK is installed correctly
* Check your import statements match the package name
* Ensure you're using the correct version for your platform

**Platform-Specific Issues**

* **Flutter**: Run `flutter doctor` to check your environment

Next Steps
----------

* `Getting Started <getting-started.html>`_ - Initialize your first project
* `Authentication Guide <guides/authentication.html>`_ - Set up user authentication
* `API Reference <flutter-sdk/api-reference.html>`_ - Explore the Flutter SDK API
