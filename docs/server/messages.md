# Messages

Currently there are two types of ***Messages*** the Noditor Server accepts: ***Alerts and Errors***. Each has it own API Endpoint. Both types require the POST body to contain at least two data keys. If an invalid Key is used the message will be rejected and the invalid Key will be reported via the Noditor App.

#### Notifications

Both Mesasge types support ***Notifications*** to your browser or mobile device. Include the optional ***notify*** parameter in the body data, set to true. The Noditor Server will do its best to prevent a race condition should your Application enter a loop that sends repeated messages. Notifications at best can be sent one per minute to any one client. Other notifications will be discarded to protect the client.


## Alerts

Alerts are usually events that might be good-to-know, such as a backend server has started or a help ticket was created.

* **key** - string: a known Key on the Noditor Server
* **msg** - string: a text message
* **notify** - boolean: (optional) defaults false

```curl
curl -d '{"key":"my-python-key", "msg":"The server has started.", "notify":true}' \
-H 'Content-Type: application/json' \
-X POST https://www.mydomain.com/alert 
```

Learn more about calling the POST /alert endpoint in the [API Reference](../api/alert-create) section of this guide.


## Errors

Errors are events that are critical-to-know, such as a database connection failed: or just about one of a million other issues.

* **key** - string: a known Key on the Noditor Server
* **err** - object: JSON objects can contain any key you want, text works as well
* **notify** - boolean: (optional) defaults false

```curl
curl -d '{"key":"my-python-key", \
          "err":{"status":500, \
                 "msg":"Internal Server error", \
                 "location":"className.methodName"}, \
          "notify":true}' \
-H 'Content-Type: application/json' \
-X POST https://www.mydomain.com/error 
```

Learn more about calling the POST /error endpoint in the [API Reference](../api/err-create) section of this guide.