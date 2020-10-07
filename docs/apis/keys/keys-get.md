# Get Keys

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
- 403 Forbidden
- 500 Internal server error
```

<!-- tabs:end -->