.. image:: logo/horizontal.svg
   :width: 480px
   :alt: websockets

|licence| |version| |pyversions| |wheel| |tests| |docs|

.. |licence| image:: https://img.shields.io/pypi/l/websockets.svg
    :target: https://pypi.python.org/pypi/websockets

.. |version| image:: https://img.shields.io/pypi/v/websockets.svg
    :target: https://pypi.python.org/pypi/websockets

.. |pyversions| image:: https://img.shields.io/pypi/pyversions/websockets.svg
    :target: https://pypi.python.org/pypi/websockets

.. |wheel| image:: https://img.shields.io/pypi/wheel/websockets.svg
    :target: https://pypi.python.org/pypi/websockets

.. |tests| image:: https://img.shields.io/github/checks-status/aaugustin/websockets/main
   :target: https://github.com/aaugustin/websockets/actions/workflows/tests.yml

.. |docs| image:: https://img.shields.io/readthedocs/websockets.svg
   :target: https://websockets.readthedocs.io/

What is ``websockets``?
-----------------------

``websockets`` is a library for building WebSocket servers_ and clients_ in
Python with a focus on correctness and simplicity.

.. _servers: https://github.com/aaugustin/websockets/blob/main/example/server.py
.. _clients: https://github.com/aaugustin/websockets/blob/main/example/client.py

Built on top of ``asyncio``, Python's standard asynchronous I/O framework, it
provides an elegant coroutine-based API.

`Documentation is available on Read the Docs. <https://websockets.readthedocs.io/>`_

Here's how a client sends and receives messages:

.. copy-pasted because GitHub doesn't support the include directive

.. code:: python

    #!/usr/bin/env python

    import asyncio
    from websockets import connect

    async def hello(uri):
        async with connect(uri) as websocket:
            await websocket.send("Hello world!")
            await websocket.recv()

    asyncio.run(hello("ws://localhost:8765"))

And here's an echo server:

.. code:: python

    #!/usr/bin/env python

    import asyncio
    from websockets import serve

    async def echo(websocket):
        async for message in websocket:
            await websocket.send(message)

    async def main():
        async with serve(echo, "localhost", 8765):
            await asyncio.Future()  # run forever

    asyncio.run(main())

Does that look good?

`Get started with the tutorial! <https://websockets.readthedocs.io/en/stable/intro/index.html>`_

.. raw:: html

    <hr>
    <img align="left" height="150" width="150" src="https://raw.githubusercontent.com/aaugustin/websockets/main/logo/tidelift.png">
    <h3 align="center"><i>websockets for enterprise</i></h3>
    <p align="center"><i>Available as part of the Tidelift Subscription</i></p>
    <p align="center"><i>The maintainers of websockets and thousands of other packages are working with Tidelift to deliver commercial support and maintenance for the open source dependencies you use to build your applications. Save time, reduce risk, and improve code health, while paying the maintainers of the exact dependencies you use. <a href="https://tidelift.com/subscription/pkg/pypi-websockets?utm_source=pypi-websockets&utm_medium=referral&utm_campaign=readme">Learn more.</a></i></p>
    <hr>
    <p>(If you contribute to <code>websockets</code> and would like to become an official support provider, <a href="https://fractalideas.com/">let me know</a>.)</p>

Why should I use ``websockets``?
--------------------------------

The development of ``websockets`` is shaped by four principles:

1. **Simplicity**: all you need to understand is ``msg = await ws.recv()`` and
   ``await ws.send(msg)``; ``websockets`` takes care of managing connections
   so you can focus on your application.

2. **Robustness**: ``websockets`` is built for production; for example it was
   the only library to `handle backpressure correctly`_ before the issue
   became widely known in the Python community.

3. **Quality**: ``websockets`` is heavily tested. Continuous integration fails
   under 100% branch coverage. Also it passes the industry-standard `Autobahn
   Testsuite`_.

4. **Performance**: memory usage is configurable. An extension written in C
   accelerates expensive operations. It's pre-compiled for Linux, macOS and
   Windows and packaged in the wheel format for each system and Python version.

Documentation is a first class concern in the project. Head over to `Read the
Docs`_ and see for yourself.

.. _Read the Docs: https://websockets.readthedocs.io/
.. _handle backpressure correctly: https://vorpus.org/blog/some-thoughts-on-asynchronous-api-design-in-a-post-asyncawait-world/#websocket-servers

Why shouldn't I use ``websockets``?
-----------------------------------

* If you prefer callbacks over coroutines: ``websockets`` was created to
  provide the best coroutine-based API to manage WebSocket connections in
  Python. Pick another library for a callback-based API.
* If you're looking for a mixed HTTP / WebSocket library: ``websockets`` aims
  at being an excellent implementation of :rfc:`6455`: The WebSocket Protocol
  and :rfc:`7692`: Compression Extensions for WebSocket. Its support for HTTP
  is minimal — just enough for a HTTP health check.

What else?
----------

Bug reports, patches and suggestions are welcome!

To report a security vulnerability, please use the `Tidelift security
contact`_. Tidelift will coordinate the fix and disclosure.

.. _Tidelift security contact: https://tidelift.com/security

For anything else, please open an issue_ or send a `pull request`_.

.. _issue: https://github.com/aaugustin/websockets/issues/new
.. _pull request: https://github.com/aaugustin/websockets/compare/

Participants must uphold the `Contributor Covenant code of conduct`_.

.. _Contributor Covenant code of conduct: https://github.com/aaugustin/websockets/blob/main/CODE_OF_CONDUCT.md

``websockets`` is released under the `BSD license`_.

.. _BSD license: https://github.com/aaugustin/websockets/blob/main/LICENSE
