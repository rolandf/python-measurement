.. include:: ../README.rst

**Contents:**

.. toctree::
   :maxdepth: 2
   :glob:

   measures
   custom_measures

Installation
============

You can install the latest version of the package with Pip::

    python3 -m pip install measurement

Usage
=====

Using Measurement Objects
-------------------------

You can import any of the above measures from :mod:`.measurement.measures`
and use it for easily handling measurements like so:

.. code-block:: python

    >>> from measurement.measures import Mass
    >>> m = Mass(lb=135) # Represents 135 lbs
    >>> print(m)
    135 lb
    >>> print(m["long ton"])
    0.06027063971456692913385826772

You can create a measurement unit using any compatible unit and can transform
it into any compatible unit.  See :doc:`measures` for information about which
units are supported by which measures.

.. seealso::
    Should you be planing to go to Mars, you might need to increase your
    `decimal precision`_, like so:

    .. code-block:: python

        >>> import decimal
        >>> decimal.getcontext().prec = 28

.. _decimal precision: https://docs.python.org/3.8/library/decimal.html

Guessing Measurements
---------------------

If you happen to be in a situation where you are processing a list of
value/unit pairs (like you might find at the beginning of a recipe), you can
use the :func:`.guess` function to give you a measurement object.:

.. code-block:: python

    >>> from measurement.utils import guess
    >>> m = guess(10, "mg")
    >>> print(repr(m))
    Mass(gram="0.010")

By default, this will check all built-in measures, and will return the first
measure having an appropriate unit.  You may want to constrain the list of
measures checked (or your own measurement classes, too) to make sure
that your measurement is not mis-guessed, and you can do that by specifying
the ``measures`` keyword argument:

.. code-block:: python

    >>> from measurement.measures import Distance, Temperature, Volume
    >>> m = guess(24, "°F", measures=[Distance, Volume, Temperature])
    >>> print(repr(m))
    Temperature(fahrenheit="24.00000000000000000000000008")

If no match is found, a :class:`ValueError` exception will be raised.

.. note::
   It is absolutely possible for this to misguess due to common measurement
   abbreviations overlapping -- for example, both Temperature and Energy
   accept the argument ``c`` for representing degrees celsius and calories
   respectively.  It is advisible that you constrain the list of measurements
   to check to ones that you would consider appropriate for your input data.


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

Icons made by Freepik_ from Flaticon_.

.. _Freepik: https://www.flaticon.com/authors/freepik
.. _Flaticon: https://www.flaticon.com/
