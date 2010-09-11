QUnitTestRunnerPlugin
=======================

QUnitTestRunnerPlugin is a plugin for [JsTestDriver][] that allows JsTestDriver
to run [QUnit][] tests.

[JsTestDriver]: http://code.google.com/p/js-test-driver/  "JsTestDriver"
[QUnit]: http://docs.jquery.com/Qunit  "QUnit"

This plugin differes from the QUnitAdapter that is bundled with JsTestDriver:
QUnitAdapter is a wrapper over the JsTestDriver framework that translates from
QUnit API calls to JsTestDriver methods.  QUnitAdapter also does not support
asynchronous tests.

QUnitTestRunnerPlugin uses the actual QUnit framework to run tests.  Therefore
the whole QUnit API is available - including asynchronous tests.  QUnit is a
well-tested framework; using it directly can help to keep your test suite as
stable as possible.


Usage
--------

Include the files qunit.js and QUnitTestRunnerPlugin.js in the load directive
in your JsTestDriver configuration file.  Make sure that both of those files
are loaded before any of your QUnit test files.  Otherwise configure and run
JsTestDriver according to the directions in [the JsTestDriver documentation][JsTestDriver].

To run a single QUnit test module at a time give the description of the module
in quotes as the value of the `--tests` option when running JsTestDriver.
Currently there is no way to run individual tests - only whole modules.

QUnitTestRunnerPlugin is configured to automatically time out async tests after
five seconds.  To modify that duration edit QUnitTestRunnerPlugin.js and change
the value of the `DEFAULT_TIMEOUT` variable.  Leave the variable undefined to
disable timeouts.  Or you can specify a custom timeout duration per test by
giving a timeout argument to the QUnit `stop()` function.


Known Issues
--------------

- QUnit does not report test execution durations to JsTestDriver.  All of your
  tests will be reported as having taken zero milliseconds to run.
