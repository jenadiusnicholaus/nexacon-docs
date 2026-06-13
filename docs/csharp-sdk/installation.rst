C# SDK Installation
===================

Requirements
------------

* .NET >= 6.0
* NuGet

Installation
------------

.. code-block:: bash

    dotnet add package Nexacon.SDK

Or add to your `.csproj` file:

.. code-block:: xml

    <PackageReference Include="Nexacon.SDK" Version="1.0.0" />

Verification
------------

Verify the installation by importing the SDK:

.. code-block:: csharp

    using Nexacon.SDK;
    Console.WriteLine("Nexacon SDK installed successfully");

Next Steps
----------

* `Quick Start <quickstart.html>`_ - Initialize your first project
* `API Reference <api-reference.html>`_ - Explore the API
