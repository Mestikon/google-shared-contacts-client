# Win32 Release #
  * No extra requirements, only download the Win32 zip file, decompress and use the shared\_contacts\_profiles.exe file within the folder


# Regular Python Release (Non Win32) #

## Requirements ##
  * Python 2.4 or higher
  * [ElementTree](http://pypi.python.org/pypi/elementtree/) Python library (builtin with Python 2.5 and higher)
  * [GData Python client library](http://code.google.com/p/gdata-python-client/) version 2.0.6 or above
  * the login and password of a Google Apps domain administrator account

## Installation Procedure ##

  1. [Download](http://code.google.com/p/google-shared-contacts-client/downloads/list) the project in your preferred format: `.tar.gz` or `.zip`.
  1. Decompress the archive on your machine. All the script files belong to a `google-shared-contacts-client/` directory.
  1. If necessary, install the GData Python client library and its dependencies. This article gives a detailed procedure: [Getting Started With the Google Data Python Library](http://code.google.com/apis/gdata/articles/python_client_lib.html).<br>You can also download the GData Python client library and move its <code>src/atom/</code> and <code>src/gdata/</code> directories to <code>google-shared-contacts-client/</code> so that the script can load the <code>atom</code> and <code>gdata</code> modules.