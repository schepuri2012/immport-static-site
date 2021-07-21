# Overview
The Data Upload API provides programmatic access to the ImmPort Data Upload
Service. This service includes requests for upload, validation, and status
information.  This API works as access for posting upload/validation
registration requests and acquiring information on the the status of a Batch
Upload. The API returns a JSON output by default, except for the
documentation request that returns a Zip-file.  The HTTP method supported by
this API is POST (-X POST) in most cases for this version of this API
(exceptions will be noted below).

## Tools for communicating with the ImmPort Data Upload API


Many third-party tools can be used for communicating with the API and for
visualizing API endpoints.

Examples of tools for communicating with the API:

| Tool      | Type   |
| ------------- |-------------|
| [Curl](http://curl.haxx.se/docs/manpage.html) | Command line tool |
| [HTTPie](http://httpie.org) | Command line tool |
| [Postman REST Client](http://www.getpostman.com/) | App for Google Chrome and OS X |
| [DHC REST Client](http://restlet.com/products/dhc/) | Google Chrome extension |
| [Google Chrome](http://www.google.com/chrome/) | Google Chrome web browser |

This document will use the curl tool for examples.