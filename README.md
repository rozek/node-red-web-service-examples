# node-red-web-server-examples #

This collection of [Node-RED](https://nodered.org/) examples (with a matching [Postman](https://www.postman.com/) collection for testing) is mainly intended for my students, but parts of it may also be of more general interest.

It is the continuation of another set of [HTTP(S)-related examples](https://github.com/rozek/node-red-http-examples) and explains how to implement some basic file-based web servers with or without custom HTTP endpoints and with or without cookie-based authorization.

For this series, it is assumed that the reader already installed Node-RED (as described in [Getting Started](https://nodered.org/docs/getting-started/)), optionally secured the editor (as shown in [Securing Node-RED](https://nodered.org/docs/user-guide/runtime/securing-node-red)) and started using it (as explained in [Creating your first flow](https://nodered.org/docs/tutorials/first-flow))

### Required Extensions ###

For these examples to be run, it is necessary to install the following extension:

* [node-red-contrib-components](https://github.com/ollixx/node-red-contrib-components)<br>"Components" allow multiply needed flows to be defined once and then invoked from multiple places

## Examples ##

All example specifications are stored in JSON format and may easily be imported into a Node-RED workspace. Preferrably, you should open a separate tab and insert them there.

To test the examples, a [Postman collection](examples/PostmanCollection.json) is included, which may easily be imported into a running [Postman](https://www.postman.com/) instance. After the import, you should open the collection's "Variables" section and set the `BaseURL` to the base URL of your NodeRED instance (by default, it is set to `127.0.0.1:1880`, which should work out-of-the-box for most Node-RED installations). If your Node-RED instance has been configured to require basic authentication, you should also set the variables `Username` and `Password`)

Alternatively, other tools like [cURL](https://curl.se/) may be used as well.

### Simple (and open) Web Server ###

The first example in this series is a simple web server delivering files found in a configured directory.

> For this example to work, please copy file `FileTypeMappings.json` and folder `public` into the working directory of your Node-RED instance

The server is principally "open" for everybody as not extra authorization is needed to get responses for sent requests.

A simple path normalization asserts that clients may only request files from within the configured directory and may not inspect the whole file system.

If the requested path is that of a directory, the client is redirected to a file "index.html" in that directory. If no file exists at the requested path, a response with the status code 404 (Not Found) is sent back.

The server recognizes many different file types by looking at their type suffixes and sets the "Content-Type" header accordingly (see file [FileTypeMappings.json](https://raw.githubusercontent.com/rozek/node-red-web-server-examples/main/FileTypeMappings.json) for the complete set) 

Unforeseen errors are caught by a generic "catch" node and result in a response with status code 500 ("Internal Server Error")

![](examples/simple-web-server.png)

Simply import the [example from this repo](examples/simple-web-server.json) into your Node-RED workspace and deploy. You may then test your server either by navigating your browser to `{{BaseURL}}/simple-web-server` or using the included Postman collection. Currently, the `public` folder contains two files only, but you are free to add as many files as you like.

> Please note: usually, it is not a good idea to use Node-RED just for static file serving - there are lots of other solutions which are even simpler to install and configure and are much more performant and secure than this example. If, however, a server with custom endpoints is needed which *also* serves some static files, this example may be quite practical.

### Custom (and still open) Web Server ###

![](examples/custom-web-server.png)
![](examples/serving-files.png)

### Closed Web Server ###

![](examples/closed-web-server-I.png)
![](examples/closed-web-server-II.png)

## License ##

[MIT License](LICENSE.md)
