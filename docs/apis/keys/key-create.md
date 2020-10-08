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

const resp = await axios.post("/key/325", {"key":"my-key"}, options)
console.log(resp.data);
  ```
<!-- tabs:end -->

---

***Response***
<!-- tabs:start -->
#### **Data**

```json
{
  "key_id":"325",
  "key":"my-key"
}
```

#### **Errors**

```text
- 201 OK
- 403 Forbidden
- 500 Internal server error
```

<!-- tabs:end -->