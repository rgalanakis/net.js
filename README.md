Net.js
======

Net.js is a minimalist network communications library for browsers.

Why?
----

To simplify fetching remote URLs via AJAX, as well as talking to JSON APIs, in one succinct interface, without dependencies on other libraries.

Usage
=====

net.js is easy to use! Just include it in your page.

    <script src="path/to/net.js"></script>
	
This makes the global 'net' object available to your scripts.

If you prefer using net.js with require.js, just add it as a dependency and away you go:

    define('mymodule', ['net'], function(net) {
	    // Your code...
	});
	
AJAX
----

net.js has a simple wrapper around AJAX that exposes a few convenience methods (these are self explanatory):

    net.ajax.get
	net.ajax.post
	net.ajax.put
	net.ajax.delete

A more generic method for making your own requests is also available:

    net.ajax.request
	
Making a Request
----------------

There are a few basic options to get started:

* url - where to make a request
* success - what to do on success
* error - what to do on error


    net.ajax.get({
      url: '/some/path',
	  success: function(results) {
	  },
	  error: function() {
        console.log('Error making request!');
	  }
	});
	

When making a raw request, you have to also add:

* method - GET, POST, PUT, etc.


    net.ajax.request({
	  method: 'GET',
      url: '/some/path',
	  success: function(results) {
        // do something with the results
	  }
	});


You can optionally set arbitrary headers on the request. This may come
in handy for setting custom headers, or setting up HTTP Auth headers.


	net.ajax.get({
	  headers: {
        'X-Custom-Header': 'custom-value'
	  }
	});


JSON
----

The JSON client is similar to AJAX, but does a little processing on the request
to serialize and deserialize JSON objects. The JSON client is handy for talking
to APIs that speak in pure JSON.


	net.json.get({
      url: '/my-data.json',
	  success: function(data) {
        console.log(data); // a deserialized JSON object
	  }
	});
	

When issuing POST or PUT, you simply supply a data object. The JSON client will serialize
it and issue the request to your endpoint as Content-Type: application/json, and the body
of the request will contain the serialized JSON.


	net.json.post({
  	  url: '/save-data',
      data: myData, // an object to be serialized
      success: function(data) {
        console.log(data); // JSON client expects JSON responses, and will return it to you.
      }
	})


Form
----

The form client is a convenience method to encode and serialize data as form POST or PUT requests.


    net.form.post({
  	  url: '/save-data',
      data: myData, // an object to be serialized as form data
      success: function(response) {
        console.log(response); // raw text response from the server
      }
    });


Supported Browsers
==================

* Google Chrome 22+ (Desktop, Android)
* Firefox 10+
* Safari 5.x+, iOS
* IE8+ (and probably 6/7, but need tests!)
* Opera

