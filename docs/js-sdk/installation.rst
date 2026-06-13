JavaScript SDK Installation
===========================

Requirements
------------

* Node.js >= 14.0.0
* npm, yarn, or pnpm

Installation
------------

**npm**

.. code-block:: bash

    npm install nexacon-sdk

**yarn**

.. code-block:: bash

    yarn add nexacon-sdk

**pnpm**

.. code-block:: bash

    pnpm add nexacon-sdk

TypeScript Support
------------------

The SDK includes TypeScript type definitions:

.. code-block:: typescript

    import { NexaconClient } from 'nexacon-sdk';

    const client: NexaconClient = new NexaconClient({
      apiKey: 'your_api_key',
      secretKey: 'your_secret_key',
    });

Browser Usage
--------------

For browser usage, you may need a bundler like Webpack, Vite, or Rollup:

.. code-block:: bash

    npm install nexacon-sdk
    npm install --save-dev webpack webpack-cli

Verification
------------

Verify the installation by importing the SDK:

.. code-block:: javascript

    const { NexaconClient } = require('nexacon-sdk');
    console.log('Nexacon SDK installed successfully');

Or with TypeScript:

.. code-block:: typescript

    import { NexaconClient } from 'nexacon-sdk';
    console.log('Nexacon SDK installed successfully');

Next Steps
----------

* `Quick Start <quickstart.html>`_ - Initialize your first project
* `API Reference <api-reference.html>`_ - Explore the API
