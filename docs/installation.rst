Installation
============

This guide provides installation instructions for all Nexacon SDKs.

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

JavaScript SDK
--------------

**Requirements**

* Node.js >= 14.0.0
* npm, yarn, or pnpm

**Installation**

.. code-block:: bash

    npm install nexacon-sdk
    # or
    yarn add nexacon-sdk
    # or
    pnpm add nexacon-sdk

**Verification**

.. code-block:: javascript

    const { NexaconClient } = require('nexacon-sdk');
    console.log('Nexacon SDK installed successfully');

React Native SDK
----------------

**Requirements**

* React Native >= 0.70.0
* React >= 18.0.0
* Node.js >= 14.0.0
* npm or yarn

**Installation**

.. code-block:: bash

    npm install nexacon-react-native-sdk
    # or
    yarn add nexacon-react-native-sdk

**Platform-Specific Setup**

For iOS:

.. code-block:: bash

    cd ios
    pod install
    cd ..

For Android:

No additional setup required.

**Verification**

.. code-block:: javascript

    import { NexaconClient } from 'nexacon-react-native-sdk';
    console.log('Nexacon React Native SDK installed successfully');

Python SDK
----------

**Requirements**

* Python >= 3.7
* pip

**Installation**

.. code-block:: bash

    pip install nexacon-sdk

**Verification**

.. code-block:: python

    from nexacon_sdk import NexaconClient
    print('Nexacon SDK installed successfully')

Java SDK
--------

**Requirements**

* Java >= 8
* Maven or Gradle

**Maven Installation**

Add to your `pom.xml`:

.. code-block:: xml

    <dependency>
        <groupId>com.nexacon</groupId>
        <artifactId>nexacon-sdk</artifactId>
        <version>1.0.0</version>
    </dependency>

**Gradle Installation**

Add to your `build.gradle`:

.. code-block:: groovy

    implementation 'com.nexacon:nexacon-sdk:1.0.0'

**Verification**

.. code-block:: java

    import com.nexacon.sdk.NexaconClient;
    System.out.println("Nexacon SDK installed successfully");

Go SDK
------

**Requirements**

* Go >= 1.16

**Installation**

.. code-block:: bash

    go get github.com/nexacon/nexacon-go-sdk

**Verification**

.. code-block:: go

    package main

    import "github.com/nexacon/nexacon-go-sdk"
    import "fmt"

    func main() {
        fmt.Println("Nexacon SDK installed successfully")
    }

PHP SDK
-------

**Requirements**

* PHP >= 7.4
* Composer

**Installation**

.. code-block:: bash

    composer require nexacon/sdk

**Verification**

.. code-block:: php

    <?php
    require 'vendor/autoload.php';
    use Nexacon\SDK\NexaconClient;
    echo "Nexacon SDK installed successfully";

Ruby SDK
--------

**Requirements**

* Ruby >= 2.7
* Bundler

**Installation**

Add to your `Gemfile`:

.. code-block:: ruby

    gem 'nexacon-sdk'

Then run:

.. code-block:: bash

    bundle install

**Verification**

.. code-block:: ruby

    require 'nexacon-sdk'
    puts 'Nexacon SDK installed successfully'

C# SDK
------

**Requirements**

* .NET >= 6.0
* NuGet

**Installation**

.. code-block:: bash

    dotnet add package Nexacon.SDK

**Verification**

.. code-block:: csharp

    using Nexacon.SDK;
    Console.WriteLine("Nexacon SDK installed successfully");

API Credentials
---------------

After installing the SDK, you will need to configure it with your API credentials:

1. Sign up for a Nexacon account at https://nexacon.com
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
* **React Native**: Ensure pods are installed for iOS
* **Python**: Check your Python version with `python --version`
* **Java**: Verify your Java version with `java -version`

Next Steps
----------

* `Getting Started <getting-started.html>`_ - Initialize your first project
* `Authentication Guide <guides/authentication.html>`_ - Set up user authentication
* `API Reference` - Explore the API for your chosen SDK
