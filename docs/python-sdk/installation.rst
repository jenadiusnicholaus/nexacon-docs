Python SDK Installation
========================

Requirements
------------

* Python >= 3.7
* pip

Installation
------------

.. code-block:: bash

    pip install nexacon-sdk

Virtual Environment
--------------------

It's recommended to use a virtual environment:

.. code-block:: bash

    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    pip install nexacon-sdk

Verification
------------

Verify the installation by importing the SDK:

.. code-block:: python

    from nexacon_sdk import NexaconClient
    print('Nexacon SDK installed successfully')

Next Steps
----------

* `Quick Start <quickstart.html>`_ - Initialize your first project
* `API Reference <api-reference.html>`_ - Explore the API
