# Delete Key

Deletes a [Key](../server/keys.md?id=Keys). Only Administrators can delete Keys.

---

<span class="method delete">DELETE</span> /key/{key_id}

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
- 403 Forbidden
- 500 Internal server error
```

<!-- tabs:end -->