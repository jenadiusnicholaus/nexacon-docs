PHP SDK Installation
====================

Requirements
------------

* PHP >= 7.4
* Composer

Installation
------------

Add to your `composer.json`:

.. code-block:: json

    {
        "require": {
            "nexacon/sdk": "^1.0.0"
        }
    }

Then run:

.. code-block:: bash

    composer install

Or use the command line:

.. code-block:: bash

    composer require nexacon/sdk

Verification
------------

Verify the installation by importing the SDK:

.. code-block:: php

    <?php
    require 'vendor/autoload.php';
    use Nexacon\SDK\NexaconClient;
    echo "Nexacon SDK installed successfully";

Next Steps
----------

* `Quick Start <quickstart.html>`_ - Initialize your first project
* `API Reference <api-reference.html>`_ - Explore the API
