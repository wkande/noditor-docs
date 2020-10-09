REST API Endpoints served by the Noditor Server.

[filename](auth.md ':include')

## Keys

***Keys*** are only used when sending messages or graph data from your Application to the Noditor Server.

- POST /alert
- POST /error
- POST /graph

You create Keys using the Noditor App. Generally, you will create a Key for each instance of a backend application and a single Key for a frontend application.

Keys provide two important functions.

- Group data into a logical bucket.
- Provides security for the API call, Keys are a secret.

Learn more about [Keys](server/config.md?id=keys) in the API Reference section of this guide.

### Get all Keys

Gets a list of [Keys](../server/keys.md?id=Keys). All keys are visible to all users. Only Administrators can create and delete Keys.

---

<span class="method get">GET</span> /keys

---

***Parameters***

| Name        | Type    | In     | Description |
| :---        | :---    | :---   | :--- |
| accept      | string  | header | application/json |
| token       | string  | header | JWT token |

---

***Usage***
<!-- tabs:start -->

#### **CURL**

```bash
curl get https://try.ourdomain.com/keys \
  -h {"accept":"application/json", token:"JUU76GF5TGJKM7KKJK"}
```

#### **Javascript**

```javascript
const options = {
  "headers": {"accept": "application/json", "token":"JUU76GF5TGJKM7KKJK"}
};

const resp = await axios.get("/keys", options)
console.log(resp.data);
  ```
<!-- tabs:end -->

---

***Response***

<!-- tabs:start -->

#### **Data**

```json
{
  "keys":[
    {"key_id":34, 
     "key":"my-key-1"
    },
    {"key_id":35, 
     "key":"my-key-2"
    }
  ]
}

```

#### **Errors**

```text
- 200 OK
- 401 Unauthorized
- 500 Internal server error
```

<!-- tabs:end -->

### Create a Key

Creates a [Key](../server/keys.md?id=Keys). Each Key must have a unique name. Once created a Key cannot be changed. If you made an error naming the Key, delete it and create another. Only Administrators can create Keys.

---

<span class="method post">POST</span> /key

---

***Parameters***

| Name        | Type    | In     | Description |
| :---        | :---    | :---   | :--- |
| accept      | string  | header | application/json |
| token       | string  | header | JWT token |
| key         | string  | body   | key text string; (0-9), (Aa-Zz), (-_), no spaces |

---

***Usage***
<!-- tabs:start -->

#### **CURL**

```bash
curl post https://try.ourdomain.com/key \
  -d '{"key":"my-key"}' \
  -h {"accept":"application/json", "token":"JUU76GF5TGJKM7KKJK"}
```

#### **Javascript**

```javascript
const options = {
  headers: "accept": "application/json", "token":"JUU76GF5TGJKM7KKJK"}
};

const resp = await axios.post("/key", {"key":"my-key"}, options)
console.log(resp.data);
```

<!-- tabs:end -->

---

***Response***

<!-- tabs:start -->

#### **Data**

```json
{
  "key_id":325,
  "key":"my-key"
}
```

#### **Errors**

```text
- 201 OK
- 401 Unauthorized
- 403 Forbidden
- 500 Internal server error
```

<!-- tabs:end -->

### Delete a Key

Deletes a [Key](../server/keys.md?id=Keys). Only Administrators can delete Keys.

---

<span class="method delete">DELETE</span> /key/:key_id

---

***Parameters***

| Name        | Type    | In     | Description |
| :---        | :---    | :---   | :--- |
| accept      | string  | header | application/json |
| token       | string  | header | JWT token |
| key_id      | integer | path   | key_id of the key |

---

***Usage***
<!-- tabs:start -->

#### **CURL**

```bash
curl delete https://try.ourdomain.com/key/325 \
  -h {"accept":"application/json", token:"JUU76GF5TGJKM7KKJK"}
```

#### **Javascript**

```javascript
const options = {
  headers: {"accept": "application/json", "token":"JUU76GF5TGJKM7KKJK"}
};

const resp = await axios.delete("/key/325", options)
console.log(resp.data);
  ```
<!-- tabs:end -->

---

***Response***

<!-- tabs:start -->

#### **Data**

```text
nothing
```

#### **Errors**

```text
- 204 No Content
- 401 Unauthorized
- 403 Forbidden
- 500 Internal server error
```

<!-- tabs:end -->

## Users

***Users*** are allowed access to the Noditor App and are created by Administrators. When accessing the Noditor App a user must go through the email-code-token challenge. See the [JWT](apis/main?id=JWT) section of this guide for more information on user authentication.

### Create a Code

Creates and sends an authentication code to a user's email address. Follow up to this endpoint by calling POST /token to get the user a JWT Token.

---

<span class="method post">POST</span> /code

---

***Parameters***

| Name        | Type    | In     | Description |
| :---        | :---    | :---   | :--- |
| accept      | string  | header | application/json |
| email       | string  | body   | user's email address |

---

***Usage***

<!-- tabs:start -->

#### **CURL**

```bash
curl post https://try.ourdomain.com/code \
  -d '{"email":"warren@wyosoft.com"}' \
  -h {"accept":"application/json"}
```

#### **Javascript**

```javascript
const options = {
  "headers": {"accept": "application/json"}
};

const resp = await axios.post("/code", {email:"warren@wyosoft.com"}, options)
console.log(resp.data);
  ```
<!-- tabs:end -->

---

***Response***
<!-- tabs:start -->

#### **Data**

```json
{
  "code":"Code sent to email address."
}

```

#### **Errors**

```text
- 200 OK
- 500 Internal server error
```

<!-- tabs:end -->

### Get a Token

Gets a JWT token using a user's email address and a code. The code was sent to the user's email address by POST /code.

---

<span class="method get">GET</span> /token

---

#### Parameters

| Name        | Type    | In     | Description |
| :---        | :---    | :---   | :--- |
| accept      | string  | header | application/json |
| email       | string  | query  | user's email address |
| code        | string  | query  | code sent to the user's email |

---

#### Usage

<!-- tabs:start -->

CURL

```bash
curl get https://try.ourdomain.com/token?email=warren@wyosoft.com&code=abc123 \
  -h {"accept":"application/json"}
```

Javascript

```javascript
const options = {
  "headers": {"accept": "application/json"}
};

const resp = await axios.get("/token?email=warren@wyosoft.com&code=abc123", options)
console.log(resp.data);
```

<!-- tabs:end -->

---

#### Response

<!-- tabs:start -->

#### **Data**

```json
{
  "email":"warren@wyosoft.com",
  "jwt":"UJGH7887HHHJLI8777..."
}

```

#### **Errors**

```text
- 200 OK
- 401 Unauthorized
- 500 Internal server error
```
<!-- tabs:end -->

### Get all Users

Gets a list of all Users. Any user can view the list of users. Only Administrators can create and delete Users.

---

<span class="method get">GET</span> /users

---

***Parameters***

| Name        | Type    | In     | Description |
| :---        | :---    | :---   | :--- |
| accept      | string  | header | application/json |
| token       | string  | header | JWT token |

---

***Usage***
<!-- tabs:start -->

#### **CURL**

```bash
curl get https://try.ourdomain.com/users \
  -h {"accept":"application/json", token:"JUU76GF5TGJKM7KKJK"}
```

#### **Javascript**

```javascript
const options = {
  "headers": {"accept": "application/json", "token":"JUU76GF5TGJKM7KKJK"}
};

const resp = await axios.get("/users", options)
console.log(resp.data);
  ```
<!-- tabs:end -->

---

***Response***

<!-- tabs:start -->

#### **Data**

```json
{
  "users":[
    {"user_id":38, 
     "email":"warren@wyosoft.com",
     "is_admin":true
    },
    {"user_id":39, 
     "email":"galye@wyosoft.com",
     "is_admin":false
    }
  ]
}

```

#### **Errors**

```text
- 200 OK
- 401 Unauthorized
- 500 Internal server error
```

<!-- tabs:end -->

### Create a User

Creates a non-admin user. Each user must have a unique email address. Only Administrators can create Users.

---

<span class="method post">POST</span> /user

---

***Parameters***

| Name        | Type    | In     | Description |
| :---        | :---    | :---   | :--- |
| accept      | string  | header | application/json |
| token       | string  | header | JWT token |
| email       | string  | body   | email address of the user |

---

***Usage***

<!-- tabs:start -->

#### **CURL**

```bash
curl post https://try.ourdomain.com/key \
  -d '{"email":"warren@wyosoft.com"}' \
  -h {"accept":"application/json", "token":"JUU76GF5TGJKM7KKJK"}
```

#### **Javascript**

```javascript
const options = {
  headers: "accept": "application/json", "token":"JUU76GF5TGJKM7KKJK"}
};

const resp = await axios.post("/user", {"email":"warren@wyosoft.com"}, options)
console.log(resp.data);
  ```
<!-- tabs:end -->

---

***Response***

<!-- tabs:start -->

#### **Data**

```json
{
  "user_id":23,
  "email":"ted@wyosoft.com"
}
```

#### **Errors**

```text
- 201 OK
- 401 Unauthorized
- 403 Forbidden
- 500 Internal server error
```

<!-- tabs:end -->

### Delete an User

Deletes a User. Can only be deleted by an administrator.

---

<span class="method delete">DELETE</span> /usee/:user_id

---

***Parameters***

| Name        | Type    | In     | Description |
| :---        | :---    | :---   | :--- |
| accept      | string  | header | application/json |
| token       | string  | header | JWT token |
| user_id     | integer | path   | user_id of the user |

---

***Usage***

<!-- tabs:start -->

#### **CURL**

```bash
curl delete https://try.ourdomain.com/user/424 \
  -h {"accept":"application/json", token:"JUU76GF5TGJKM7KKJK"}
```

#### **Javascript**

```javascript
const options = {
  headers: {"accept": "application/json", "token":"JUU76GF5TGJKM7KKJK"}
};

const resp = await axios.delete("/user/424", options)
console.log(resp.data);
```

<!-- tabs:end -->

---

***Response***

<!-- tabs:start -->

#### **Data**

```text
nothing
```

#### **Errors**

```text
- 204 No Content
- 401 Unauthorized
- 403 Forbidden
- 500 Internal server error
```

<!-- tabs:end -->

## Messages

***Messages*** are sent from your Applications and require a Key for authorization and data grouping. Messages are viewed from the Noditor App and require a JWT to be accessed.

### Create an Alert

Creates an Alert. Call this API from your frontend or backend Appliciations. Learn more about [Alerts](server/config?id=Alerts) in this guide.

---

<span class="method post">POST</span> /alert

---

***Parameters***

| Name        | Type    | In     | Description |
| :---        | :---    | :---   | :--- |
| accept      | string  | header | application/json |
| key         | string  | body   | key text string; (0-9), (Aa-Zz), (-_), no spaces |
| msg         | string  | body   | msg text string |
| notify      | boolean | body   | indicates a notification should be sent to the user |

---

***Usage***
<!-- tabs:start -->

#### **CURL**

```bash
curl post https://try.ourdomain.com/alert \
  -d '{"key":"my-key", "msg":"The server has started.", "notify":true}' \
  -h {"accept":"application/json"}
```

#### **Javascript**

```javascript
const options = {
  headers: "accept": "application/json"}
};

const resp = await axios.post("/alert", {"key":"my-key", "msg":"The server has started", "notify":true}, options)
console.log(resp.data);
  ```
<!-- tabs:end -->

---

***Response***

<!-- tabs:start -->

#### **Data**

```json
{
  "key_id":325,
  "key":"my-key",
  "msg_id":6757,
  "msg":"The server has started",
  "notify":true
}
```

#### **Errors**

```text
- 201 OK
- 401 Unauthorized
- 403 Forbidden
- 500 Internal server error
```

<!-- tabs:end -->

### Delete an Alert


Deletes an Alert. Can be deleted by any user or administrator.

---

<span class="method delete">DELETE</span> /alert/:alert_id

---

***Parameters***

| Name        | Type    | In     | Description |
| :---        | :---    | :---   | :--- |
| accept      | string  | header | application/json |
| token       | string  | header | JWT token |
| alert_id    | integer | path   | alert_id of the alert |

---

***Usage***

<!-- tabs:start -->

#### **CURL**

```bash
curl delete https://try.ourdomain.com/alert/4234 \
  -h {"accept":"application/json", token:"JUU76GF5TGJKM7KKJK"}
```

#### **Javascript**

```javascript
const options = {
  headers: {"accept": "application/json", "token":"JUU76GF5TGJKM7KKJK"}
};

const resp = await axios.delete("/alert/4234", options)
console.log(resp.data);
```

<!-- tabs:end -->

---

***Response***

<!-- tabs:start -->

#### **Data**

```text
nothing
```

#### **Errors**

```text
- 204 No Content
- 401 Unauthorized
- 403 Forbidden
- 500 Internal server error
```
<!-- tabs:end -->

### Create an Error

Creates an Error. Call this API from your frontend or backend Appliciations. Learn more about [Errors](server/config?id=Alerts) in this guide.

---

<span class="method post">POST</span> /error

---

***Parameters***

| Name        | Type    | In     | Description |
| :---        | :---    | :---   | :--- |
| accept      | string  | header | application/json |
| key         | string  | body   | key text string; (0-9), (Aa-Zz), (-_), no spaces |
| err         | object  | body   | any object including a string, prefer JSON
| notify      | boolean | body   | indicates a notification should be sent to the user |

---

***Usage***
<!-- tabs:start -->

#### **CURL**

```bash
curl post https://try.ourdomain.com/alert \
  -d '{"key":"my-key", "err":{"msg":"The server has started.", "location":"className.methodName"}, "notify":true}' \
  -h {"accept":"application/json"}
```

#### **Javascript**

```javascript
const options = {
  headers: "accept": "application/json"}
};

const resp = await axios.post("/alert", 
  {"key":"my-key", 
   "err":{"msg":"The server has started.", 
   "location":"className.methodName"}, 
   "notify":true}, 
   options)
console.log(resp.data);
  ```
<!-- tabs:end -->

---

***Response***

<!-- tabs:start -->

#### **Data**

```json
{
  "key_id":3445,
  "key":"my-key",
  "err_id":45456,
  "err":{"msg":"The server has started.", "location":"className.methodName"},
  "notify":true
}
```

#### **Errors**

```text
- 201 OK
- 401 Unauthorized
- 403 Forbidden
- 500 Internal server error
```

<!-- tabs:end -->

### Delete an Error


Deletes an Error. Can be deleted by any user or administrator.

---

<span class="method delete">DELETE</span> /error/:error_id

---

***Parameters***

| Name        | Type    | In     | Description |
| :---        | :---    | :---   | :--- |
| accept      | string  | header | application/json |
| token       | string  | header | JWT token |
| error_id    | integer | path   | error_id of the error |

---

***Usage***

<!-- tabs:start -->

#### **CURL**

```bash
curl delete https://try.ourdomain.com/error/1234 \
  -h {"accept":"application/json", token:"JUU76GF5TGJKM7KKJK"}
```

#### **Javascript**

```javascript
const options = {
  headers: {"accept": "application/json", "token":"JUU76GF5TGJKM7KKJK"}
};

const resp = await axios.delete("/error/1234", options)
console.log(resp.data);
```

<!-- tabs:end -->

---

***Response***

<!-- tabs:start -->

#### **Data**

```text
nothing
```

#### **Errors**

```text
- 204 No Content
- 401 Unauthorized
- 403 Forbidden
- 500 Internal server error
```

<!-- tabs:end -->

## Graphs

Graph data is sent from your Applications and requires a Key for authorization and data grouping. Graphs are viewed from the Noditor App and require a JWT to be accessed.

The name assign to graph data determines which graph the value of the graph data will appear in. Learn more about [Graphs](server/graphs?id=Graphs) in this guide.

### Create a Graph Entry

Creates a Graph Entry which is a single point on a graph. Call this API from your frontend or backend Applications.

The ***name*** of the graph is used to group the value and previously submitted values together using the name into one logical graph/chart.

---

<span class="method post">POST</span> /graph

---

***Parameters***

| Name        | Type      | In     | Description |
| :---        | :---      | :---   | :--- |
| accept      | string    | header | application/json |
| key         | string    | body   | key text string; (0-9), (Aa-Zz), (-_), no spaces |
| name        | object    | body   | name of the graph
| ts          | timestamp | body   | indicates a notification should be sent to the user |
| value       | number    | body   | a number to place on the chart, asssociated to the timestamp |

---

***Usage***
<!-- tabs:start -->

#### **CURL**

```bash
curl post https://try.ourdomain.com/graph \
  -d '{"key":"my-key", "name":"my-graph", "ts":now(), "value":13}' \
  -h {"accept":"application/json"}
```

#### **Javascript**

```javascript
const options = {
  headers: "accept": "application/json"}
};

const resp = await axios.post("/graph",
  {"key":"my-key", 
   "name":"my-graph", 
   "ts":now(),
   "value":13},
   options)
console.log(resp.data);
  ```
<!-- tabs:end -->

---

***Response***

<!-- tabs:start -->

#### **Data**

```json
{ "key_id":34,
  "key":"my-key",
  "graph_id":3445,
  "name":"my-graph",
  "ts":now(),
  "value":13
}
```

#### **Errors**

```text
- 201 OK
- 401 Unauthorized
- 403 Forbidden
- 500 Internal server error
```

<!-- tabs:end -->


### Delete a Graph

Deletes a Graph and all of the graph data associated with it by its ***name***. The graph will be re-created shoild POST /graph be called again using the same name. Can be deleted by any user or administrator.

---

<span class="method delete">DELETE</span> /graph/:name

---

***Parameters***

| Name        | Type    | In     | Description |
| :---        | :---    | :---   | :--- |
| accept      | string  | header | application/json |
| token       | string  | header | JWT token |
| name        | integer | path   | name of the graph |

---

***Usage***

<!-- tabs:start -->

#### **CURL**

```bash
const name = "my-graph";
curl delete https://try.ourdomain.com/graph/name \
  -h {"accept":"application/json", token:"JUU76GF5TGJKM7KKJK"}
```

#### **Javascript**

```javascript
const options = {
  headers: {"accept": "application/json", "token":"JUU76GF5TGJKM7KKJK"}
};

const resp = await axios.delete("/graph/my-graph", options)
console.log(resp.data);
```

<!-- tabs:end -->

---

***Response***

<!-- tabs:start -->

#### **Data**

```text
nothing
```

#### **Errors**

```text
- 204 No Content
- 401 Unauthorized
- 403 Forbidden
- 500 Internal server error
```

<!-- tabs:end -->

### Delete a Graph Entry

Deletes a Graph entry or a piece of graphj data. Can be deleted by any user or administrator.

---

<span class="method delete">DELETE</span> /graph/:graph_id

---

***Parameters***

| Name        | Type    | In     | Description |
| :---        | :---    | :---   | :--- |
| accept      | string  | header | application/json |
| token       | string  | header | JWT token |
| graph_id    | integer | path   | graph_id of the graph entry |

---

***Usage***

<!-- tabs:start -->

#### **CURL**

```bash
curl delete https://try.ourdomain.com/graph/1234 \
  -h {"accept":"application/json", token:"JUU76GF5TGJKM7KKJK"}
```

#### **Javascript**

```javascript
const options = {
  headers: {"accept": "application/json", "token":"JUU76GF5TGJKM7KKJK"}
};

const resp = await axios.delete("/graph/1234", options)
console.log(resp.data);
```

<!-- tabs:end -->

---

***Response***

<!-- tabs:start -->

#### **Data**

```text
nothing
```

#### **Errors**

```text
- 204 No Content
- 401 Unauthorized
- 403 Forbidden
- 500 Internal server error
```

<!-- tabs:end -->

---

---

---
