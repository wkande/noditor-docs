# SQLite3 Database

The Noditor Server creates a local ***SQLite3 Database*** to record data from your Applciations and other data created by the Noditor App.

This database is automatically managed by the Noditor Server. Only the TTL (Time-To-Live) parameter can be altered.

## Time-To-Live

By default the Noditor Server deletes any data older than seven days. You can adjust this value in the noditor.json config file.

The noditor.json file is not included in the cloned noditor-server repo. You must create it in the project root and enter a JSON object using the following structure. The ***ttl*** key is optional. You can set it to keep data for any duration except forever. Set the value in days.

```json
{
  "administrators":["warren@wyosoft.com"],
  "ttl":30,
  "allowed_addresses":["*"]
}
```

Changing the ttl value **does not** require the server to be restarted.

Learn more about the [noditor.json](../server/config.md?id=Configuration) file in the Noditor Server section of this guide.

## Database Tables

| Name        | Description |
| :---        | :--- |
| USERS       | Authorized email addresses that can use the Noditor App. |
| KEYS        | Known keys than can send messages and graph data to the Noditor Server. |
| ALERTS      | Alert messages sent to the Noditor Server. |
| ERRORS      | Error messages sent to the Noditor Server. |
| GRAPHS      | Graph data sent to the Noditor Server. |
| INTERNALS   | Noditor Server internal messages sent to the Noditor App. |

```mermaid
classDiagram
    class Users
    Users : user_id integer
    Users : email string
    Users : code string

```

```mermaid
classDiagram

    class Keys
    Keys : key_id integer
    Keys : key string
    Keys : alert_cnt integer
    Keys : error_cnt integer
    Keys : internal_cnt integer

    class Alerts
    Alerts : alert_id integer
    Alerts : key_id integer
    Alerts: msg string
    Alerts: notify boolean
    Alerts: ts timestamp

    class Errors
    Errors: error_id integer
    Errors: key_id integer
    Errors: err object
    Errors: notify boolean
    Errors: ts timestamp

    class Graphs
    Graphs: graph_id integer
    Graphs: key_id integer
    Graphs: graph object
    Graphs: ts timestamp

    class Internals
    Internals: internal_id integer
    Internals: key_id integer
    Internals: msg string
    Internals: ts timestamp

    Keys --> Alerts : 1 .. many
    Keys --> Errors : 1 .. many
    Keys --> Graphs : 1 .. many
    Keys --> Internals : 1 .. many


```
