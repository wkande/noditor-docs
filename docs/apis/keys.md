## Keys

Keys are used to provide three important functions when using them in an API call to send messages and graph data to theNoditor Server.

- Identifies a group data together.

- Provides security for the API call, Keys are a secret.

<!----------------------------------------------------------------->

### Get Keys

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

<!----------------------------------------------------------------->

### Create Key

Creates a [Key](../server/keys.md?id=Keys). Each Key must have a unique name. Once created a Key cannot be changed. If you made an error naming the Key, delete it and create another. Only Administrators can create Keys.

---

<span class="method delete">POST</span> /key

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

<!----------------------------------------------------------------->

### Delete Key

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