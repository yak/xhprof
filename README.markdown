XHPROF UI FORK WITH POSTGRESQL AND TIDEWAYS PHP PROFILER (PHP7) SUPPORT
=======================================================================

PostgreSQL support for Paul Reinheimer's fork of the official, and now unmaintained, Facebook XHProf UI was submitted as
a pull request in Feb 2013 (<https://github.com/preinheimer/xhprof/pull/63>). That request is as of Jan 2018 still open.

As I found myself wanting to continue using this GUI together with the PHP7 compatible Tideways PHP Profiler
(<https://github.com/tideways/php-profiler-extension>) I went ahead and added that support to this fork. 

Note that Reinheimer's fork was also patched to support Tideways but still does not have PostgreSQL support.

In short: this is an old codebase without namespaces and rife with globals, but if you wish to use PostgreSQL and PHP7,
it is a working solution.

ORIGINAL README FROM PREINHEIMER
--------------------------------

This branch/clone/whatever git calls it of the official Facebook GUI does a few things:

* It includes a header.php document you can use with PHP's
  auto\_prepend\_file directive. It sets up profiling by initilizing a few variables, and settting register_shutdown_function with the fooder. Once started profiles are done
  when requested (?\_profile=1), or randomly. Profiled pages display a link to
  their profile results at the bottom of the page (this can be disabled on a
  black list bases for specific documents. e.g. pages generating XML, images,
  etc.).
* For tips on including header.php on an nginx + php-fpm install take a look at: http://www.justincarmony.com/blog/2012/04/23/php-fpm-nginx-php_value-and-multiple-values/
* The GUI is a bit prettier (Thanks to Graham Slater)
* It uses a MySQL backend, the database schema is stored in xhprof\_runs.php
* There's a front end to view different runs, compare runs to the same url, etc.

Key features include:

* Listing 25, 50 most recent runs
* Display most expensive (cpu), longest running, or highest memory usage runs
  for the day
* It introduces the concept of "Similar" URLs. Consider:
  * http://news.example.com/?story=23
  * http://news.example.com/?story=25
  While the URLs are different, the PHP code execution path is likely identical,
  by tweaking the method in xhprof\_runs.php you can help the front end be aware
  that these urls are identical.
* Highcharts is used to graph stats over requests for an
  easy heads up display.

Requirements:

* Zlib library in PHP: <http://php.net/manual/en/zlib.installation.php>
  (Used to compress serialized data)
* Database backend
* MySQL, or MySQLi for data storage fully supported
* Support for SQL Server now in beta stages #jumpInCamp

Work that we're still doing:

* The aggregation functionality is ignored completely
* The code is... a mess. Deadlines do that to you, we're working on it
* The default table schema isn't indexed all the places it needs to be
* Easier ways to diff URLs
