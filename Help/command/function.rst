function
--------

Start recording a function for later invocation as a command.

.. code-block:: cmake

  function(<name> [<arg1> ...])
    <commands>
  endfunction()

Defines a function named ``<name>`` that takes arguments
named ``<arg1>``, ...
The ``<commands>`` in the function definition are recorded;
they are not invoked until the function is invoked. When
the function is invoked, the recorded ``<commands>`` are first
modified by replacing formal parameters (``${arg1}``, ...)
with the arguments passed, and then invoked as normal commands.

In addition to referencing the formal parameters you can reference the
``ARGC`` variable which will be set to the number of arguments passed
into the function as well as ``ARGV0``, ``ARGV1``, ``ARGV2``, ...  which
will have the actual values of the arguments passed in.
This facilitates creating functions with optional arguments.

Furthermore, ``ARGV`` holds the list of all arguments given to the
function and ``ARGN`` holds the list of arguments past the last expected
argument.
Referencing to ``ARGV#`` arguments beyond ``ARGC`` have undefined
behavior. Checking that ``ARGC`` is greater than ``#`` is the only way
to ensure that ``ARGV#`` was passed to the function as an extra
argument.

Per legacy, the :command:`endfunction` command admits an optional
``<name>`` argument. If used, it must be a verbatim repeat of the
argument of the opening ``function`` command.

A function opens a new scope: see :command:`set(var PARENT_SCOPE)` for
details.

See the :command:`cmake_policy()` command documentation for the behavior
of policies inside functions.
