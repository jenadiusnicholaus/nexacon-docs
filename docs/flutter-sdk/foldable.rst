Foldable Devices
================

The foldable device service provides functionality for detecting and responding to fold state changes on Android foldable devices.

For detailed API reference, see `API Reference <api-reference.html#foldstateservice>`_.

Features
--------

* **Detect Fold State** - Check current fold state (flat, folded, half-open)
* **Fold State Stream** - Listen for fold state changes
* **State Queries** - Query specific states (isFolded, isFlat, isHalfOpen)

Quick Example
-------------

.. code-block:: dart

    // Get current fold state
    final foldState = client.foldStateService.currentState;
    print('Fold state: $foldState');

    // Listen for fold state changes
    client.foldStateService.foldStateStream.listen((state) {
      print('Fold state changed: $state');
    });
