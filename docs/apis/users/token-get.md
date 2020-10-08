### Get a Token

Gets a JWT token using a user's email address and a code. The code was sent to the user's email address by GET /code.

---

<span class="method get">GET</span> /token

---

***Parameters***

| Name        | Type    | In     | Description |
| :---        | :---    | :---   | :--- |
| accept      | string  | header | application/json |
| email       | string  | query  | user's email address |
| code        | string  | query  | code sent to the user's email |

---

***Usage***
<!-- tabs:start -->

#### **CURL**

```bash
curl get https://try.ourdomain.com/token?email=warren@wyosoft.com&code=abc123 \
-h {"accept":"application/json"}
```

#### **Javascript**

```javascript
const options = {
  "headers": {"accept": "application/json"}
};

const resp = await axios.get("/token?email=warren@wyosoft.com&code=abc123", options)
console.log(resp.data);
  ```
<!-- tabs:end -->

---

***Response***
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
- 403 Forbidden
- 500 Internal server error
```

<!-- tabs:end -->