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