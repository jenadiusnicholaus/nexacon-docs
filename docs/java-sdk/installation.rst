Java SDK Installation
=====================

Requirements
------------

* Java >= 8
* Maven or Gradle

Installation
------------

**Maven**

Add to your `pom.xml`:

.. code-block:: xml

    <dependency>
        <groupId>com.nexacon</groupId>
        <artifactId>nexacon-sdk</artifactId>
        <version>1.0.0</version>
    </dependency>

**Gradle**

Add to your `build.gradle`:

.. code-block:: groovy

    implementation 'com.nexacon:nexacon-sdk:1.0.0'

Android Setup
-------------

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

.. code-block:: java

    import com.nexacon.sdk.NexaconClient;
    System.out.println("Nexacon SDK installed successfully");

Next Steps
----------

* `Quick Start <quickstart.html>`_ - Initialize your first project
* `API Reference <api-reference.html>`_ - Explore the API
