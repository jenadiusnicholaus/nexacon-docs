Calls
=====

The calling service provides audio and video calling capabilities using WebRTC for peer-to-peer and group calls.

For detailed API reference, see `API Reference <api-reference.html#calls>`_.

Features
--------

* **P2P Calls** - One-to-one audio and video calls
* **Group Calls** - Multi-participant calls
* **WebRTC** - Real-time communication
* **Call Controls** - Mute, speaker, camera switch
* **Call Duration** - Track call duration

Quick Example
-------------

.. code-block:: ruby

    # Initiate a video call
    call = client.calls.initiate_call('+255788811191', 'video', 'my-room')

    # End the call
    client.calls.end_call(call['call_id'])

See `Quick Start <quickstart.html>`_ for more examples.
