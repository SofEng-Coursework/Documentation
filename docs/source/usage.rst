Usage
=====

.. _installation:

Installation
------------

To use VueQueue, it is as easy as installing the application on your phone, and registering a new account!

.. code-block:: console

   (.venv) $ pip install VueQueue

Joining Queues
----------------

To join a queue, scan the QR code provided by an organisation that supports VueQueue:

The ``QR`` code should be either ``valid`` or ``invalid``,
. If it is invalid, the application will throw an error message informing 
the user about the situation.

.. autoexception:: lumache.InvalidKindError

For example:

>>> Launch Application
>>> Scan QR Code
>>> Join Queue

