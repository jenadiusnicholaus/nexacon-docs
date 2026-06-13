React Native SDK Installation
=============================

Requirements
------------

* React Native >= 0.70.0
* React >= 18.0.0
* Node.js >= 14.0.0
* npm or yarn

Installation
------------

**npm**

.. code-block:: bash

    npm install nexacon-react-native-sdk

**yarn**

.. code-block:: bash

    yarn add nexacon-react-native-sdk

Platform-Specific Setup
-----------------------

iOS
^^^

Install iOS pods:

.. code-block:: bash

    cd ios
    pod install
    cd ..

Add the following to your `ios/Runner/Info.plist`:

.. code-block:: xml

    <key>NSCameraUsageDescription</key>
    <string>Camera access is required for video calls</string>
    <key>NSMicrophoneUsageDescription</key>
    <string>Microphone access is required for audio calls</string>

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

Verification
------------

Verify the installation by importing the SDK:

.. code-block:: typescript

    import { NexaconClient } from 'nexacon-react-native-sdk';
    console.log('Nexacon React Native SDK installed successfully');

Next Steps
----------

* `Quick Start <quickstart.html>`_ - Initialize your first project
* `API Reference <api-reference.html>`_ - Explore the API
