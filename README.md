logmatch
========

The `logmatch` program is a tool written in Python for parsing and filtering logging files.

By default, it handles both Syslog and NCSA log formats, but can be extended by defining new format files.

Its code is available at [Github][0], and is licensed under the terms of the [BSD license][1].

**Requirements:**

* Python 2.6+
* python-dateutil

**Usage:**

	Usage: logmatch [OPTIONS] -f FORMAT [FILTER]

	Logging file filter and parser.

	Options:
	   -c, --config      configuration directory path
	   -f, --format      log file format (use `?' to list formats)
	   -d, --display     output display fields (separated by commas)
	   -h, --help        display this help and exit
	   -i, --input-file  input log file (defaults to STDIN)
	   -l, --list        list available fields
	   -s, --separator   output display separator (defaults to space)

**Examples:**

Parsing data:

	$ logmatch -f ncsa -i /var/log/nginx/access.log -d status,request_uri
	200 /
	404 /sitemaps.xml
	200 /
	200 /favicon.ico
	200 /robots.txt
	401 /admin
	200 /about.html
	200 /

Filtering data:

	$ logmatch -f ncsa -i /var/log/nginx/access.log 'status != 200'
	1.2.3.4 - - [01/Jan/1970:00:00:00 +0100] "GET /sitemaps.xml HTTP/1.1" 404 116 "-" "GreatUserAgent/1.0"
	1.2.3.4 - - [01/Jan/1970:00:00:00 +0100] "GET /admin HTTP/1.1" 401 110 "-" "GreatUserAgent/1.0"

Parsing and filtering data:

	$ logmatch -f ncsa -i /var/log/nginx/access.log -d status,request_uri 'status != 200'
	404 /sitemaps.xml
	401 /admin


[0]: http://github.com/vbatoufflet/logmatch
[1]: http://opensource.org/licenses/BSD-3-Clause
