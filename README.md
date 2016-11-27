A wrapper for Express that adds the things it boneheadedly leaves out by default:

```javascript
var WebSite = require("web-site")

var site = new WebSite()
site.addRoute("get", "/", function(x,response) {
  response.send("okay")
})
site.start(4100)
site.stop()
```

# Why

In the name of modularity, Express has stopped doing basic HTTP server things by default. I don't want to have to configure an express server every time I want to start it on a port, parse a cookie, parse a JSON body, etc. These things are the most basic, fundamental activities of an HTTP server, it's OK to load them by default.

# Features

* Adds bodyParser by default
* Adds cookieParser by default
* site.stop()
* site.isStarted()
* site.getPort()

If you want to tell the web site to use a different http server, you can ask it to relinquish control of starting and stopping:

    var site = new WebSite()
    site.addRoute(...)

    site.relinquishControl(function() {
      var httpServer = ...

      // we can start this here, or wait, or whatever

      // Then we return the httpServer so the routes can go into that instead:
      return httpServer
    }
