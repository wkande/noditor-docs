## Authorization

The API Endpoints are protected by two different mechanisim. Keys and Address Checking are used when sending data from your Application. JWT Tokens are used by the Noditor App to access data.

* **Keys and Address Checking** - Sending message and graph data from Applications
* **JWT** - Data access by the Noditor App (or any client you might create)


### Keys/Addresses

Data submission endpoints are protected by a ***Key*** and optionally by ***Address*** checking.

The following API endpoints require a valid key to succeed.

* POST /alert
* POST /error
* POST /graph

#### Keys

The above endpoints are used to POST data to the Noditor Server. Keys are created by users with the Noditor App. Use of an invalid Key will result in a response error and the invalid Key is reported to users of the Noditor App.

```javascript
import axios from "axios";

let res = await axios.post("https://www.yourdominan.com/alert", 
  {
    "key":"my-app-key", 
    "msg":"The server has started"
  },
  {"timeout":200}
);
console.log(res.data);
```

#### Address Checking (optional)

If you host the Noditor Server in the cloud ***Address Checking*** should be implemented. When your Application submits data with one of the three POST endpoints, the Address of the requesting server is checked against the allow_addresses array declared in the ***noditor.json*** file. Use ip or hostnames. Wildcards are permitted only at the start or end of the address.

```json
{
  "administrators":["warren@wyosoft.com"],
  "allowed_addresses":["192.168.0.14","*.mydomain.com"]
}
```

Learn more about the [noditor.json](server/main.md?id=Configuration) file in the Noditor Server section of this guide.

### JWT

JSON Web Tokens are used to secure API data access by the Noditor App (or any client you might like to create).

The ***Token*** is granted using the email-code-token challenge mechanism. This process is handled by the Noditor App and the POST /code and GET /token endpoints.

* The user enters their email address. If it is a known email address (added by an administrator using the Noditor App) then a code is sent to the email address.

* The user then enters the code and a JWT token is returned.

* Future requests by the Noditor App will add the JWT token to the request header for each API endpoint call.

When an endpoint receives a request from the Noditor App the JWT token is decrypted and the embedded email is checked against the list of known email addresses. Had the email address been removed from the known list of email addresses after the token was issued the request will fail.

Logout a user by deleting the JWT token at the client as does the Noditor App.
