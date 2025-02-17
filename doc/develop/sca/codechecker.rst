.. _codechecker:

CodeChecker support
###################

`CodeChecker <https://codechecker.readthedocs.io/>`__ is a static analysis infrastructure.
It executes analysis tools available on the build system, such as
`Clang-Tidy <http://clang.llvm.org/extra/clang-tidy/>`__,
`Clang Static Analyzer <http://clang-analyzer.llvm.org/>`__ and
`Cppcheck <https://cppcheck.sourceforge.io/>`__. Refer to the analyzer's websites for installation
instructions.

Installing CodeChecker
**********************

CodeChecker itself is a python package available on `pypi <https://pypi.org/project/codechecker/>`__.

.. code-block:: shell

    pip install codechecker

Running with CodeChecker
************************

To run CodeChecker, :ref:`west build <west-building>` should be
called with a ``-DZEPHYR_SCA_VARIANT=codechecker`` parameter, e.g.

.. code-block:: shell

    west build -b mimxrt1064_evk -s samples/basic/blinky -- -DZEPHYR_SCA_VARIANT=codechecker


Configuring CodeChecker
***********************

To configure CodeChecker or analyzers used, arguments can be passed using the
``CODECHECKER_ANALYZE_OPTS`` parameter, e.g.

.. code-block:: shell

    west build -b mimxrt1064_evk -s samples/basic/blinky -- -DZEPHYR_SCA_VARIANT=codechecker \
    -DCODECHECKER_ANALYZE_OPTS="--config;$CODECHECKER_CONFIG_FILE;--timeout;60"


Exporting CodeChecker reports
*****************************

Optional reports can be generated using the CodeChecker results, when passing a
``-DCODECHECKER_EXPORT=<type>`` parameter. Allowed types are: ``html,json,codeclimate,gerrit,baseline``.
Multiple types can be passed as comma-separated arguments.

Optional parser configuration arguments can be passed using the
``CODECHECKER_PARSE_OPTS`` parameter, e.g.

.. code-block:: shell

    west build -b mimxrt1064_evk -s samples/basic/blinky -- -DZEPHYR_SCA_VARIANT=codechecker \
    -DCODECHECKER_EXPORT=html,json -DCODECHECKER_PARSE_OPTS="--trim-path-prefix;$PWD"
