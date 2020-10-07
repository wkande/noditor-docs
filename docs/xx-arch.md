# Architecture


***Applications*** (your frontend or backend applications) push messages and graph data directly to the Noditor Server.  

The ***Noditor Server*** stores everything locally in a SQLite3 database. Applications written in any language will work as long as they can communicate with the Noditor Server using HTTPS. You can host the Noditor Sever anywhere you want. It only contains your data and is managed by the Noditor Mobile App.

The ***Noditor Mobile App*** (PWA) will access the Noditor Server to render graphs and list messages. 


```mermaid
graph TB

    A[fa:fa-code Frontend/Backend Applications] --> |Graph Data| B[fa:fa-server Noditor Server]

    A -->| Messages | B
    B --> C[fa:fa-mobile Noditor Mobile App]
    C --> B
    style A fill:#f9f9,stroke:gray,stroke-width:1px
    style B fill:#C0D9AF,stroke:gray,stroke-width:1px
    style C fill:#C0D9AF,stroke:gray,stroke-width:1px
```



