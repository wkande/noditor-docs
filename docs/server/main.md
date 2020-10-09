The ***Noditor Server*** accepts messages and graph data frm your Applications. The data is redenered wihtthe ***Noditor App** or your own client using the APIs.

## Configuration

On startup the Noditor Server reads from the ***noditor.json*** config file. The noditor.json file is not included in the cloned noditor-server repo. You must create it in the project root and enter a JSON object using the following structure. The **administrators** and **allowed_addresses** are required.


```json
{
  "administrators":["warren@wyosoft.com"],
  "ttl":7,
  "allowed_addresses":["192.168.0.14", "*.mydomain.com"]
}
```

#### Options

* **administrators**:array (required) - An array of email addresses that are granted full admin privileges when using the Noditor App.

* **ttl**:int (optional) - The Time-To-Live value (in days) for message and graph data to live in the local SQLite3 database. Set it to keep data for any duration except forever. Defaults to 7. 

* **allowed_addresses**:array (required) - A white list of addresses that the Noditor Server will accept message and graph data from. Wild card usage is accepted using (*) only at the start or end of the address.

  The following would allow all addresses.

  ```json
  {
    "administrators":["warren@wyosoft.com"],
    "ttl":7,
    "allowed_addresses":["*"]
  }

  // Other examples
  // 192.168.0.*
  // *.mydomain.com
  ```

[filename](keys.md ':include')

[filename](messages.md ':include')

[filename](graphs.md ':include')

[filename](db.md ':include')