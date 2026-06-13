Flutter SDK Installation
========================

Requirements
------------

* Flutter SDK >= 3.0.0
* Dart SDK >= 3.0.0
* Platform-specific requirements:
  * Android: Android Studio and Android SDK
  * iOS: Xcode 14+ (macOS only)
  * Linux: GTK development libraries
  * macOS: Xcode command-line tools
  * Windows: Visual Studio 2022 with C++ workload
  * Web: Chrome or Edge browser

Installation
------------

Add the SDK to your Flutter project:

.. code-block:: bash

    flutter pub add nexacon_sdk

Or add it manually to your `pubspec.yaml`:

.. code-block:: yaml

    dependencies:
      nexacon_sdk: ^1.1.4

Platform Configuration
---------------------

Android
^^^^^^^

Add the following to your `android/app/build.gradle`:

.. code-block:: groovy

    android {
        defaultConfig {
            minSdkVersion 21
        }
    }

Add required permissions to `android/app/src/main/AndroidManifest.xml`:

.. code-block:: xml

    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.RECORD_AUDIO" />
    <uses-permission android:name="android.permission.CAMERA" />
    <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />

iOS
^^^

Add the following to your `ios/Runner/Info.plist`:

.. code-block:: xml

    <key>NSCameraUsageDescription</key>
    <string>Camera access is required for video calls</string>
    <key>NSMicrophoneUsageDescription</key>
    <string>Microphone access is required for audio calls</string>

Web
^^^

No additional configuration required.

Linux
^^^^^

Install GTK development libraries:

.. code-block:: bash

    sudo apt-get install libgtk-3-dev libglib2.0-dev

macOS
^^^^^

No additional configuration required.

Windows
^^^^^^^

Install Visual Studio 2022 with the C++ workload.

Verification
------------

Verify the installation by importing the SDK:

.. code-block:: dart

    import 'package:nexacon_sdk/nexacon_sdk.dart';

    void main() {
      print('Nexacon SDK installed successfully');
    }

Next Steps
----------

* `Quick Start <quickstart.html>`_ - Initialize your first project
* `API Reference <api-reference.html>`_ - Explore the API
