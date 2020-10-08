# Getting Started

* Install the Noditor Server
* Run the Noditor App
* Send a Message

## Noditor Server

The installation process to setup the Noditor Server is straight forward. Simply clone the Noditor Server from its GitHub repo, install dependencies, create the noditor.json config file and start the server. When the server starts for the first time it will create the SQLite3 database it uses to store data send from your applications.

1. **Clone the Repo**

```json
git clone git@github.com:wkande/noditor-server.git
cd noditor-server
```

2. **Configuration**

The ***Noditor Server*** reads from the ***noditor.json*** file at startup. The noditor.json file is not included in the cloned repo. You must create it in the project root and enter a JSON object using the following structure. The adminstrators must be a know at startup. Changing the known Administrators does require that the server be restarted.

Learn more about the [noditor.json](../server/config.md?id=Configuration) file in the Noditor Server section of this guide.

```json
{
  "administrators":["warren@wyosoft.com"],
  "allowed_adresses":["*"]
}
```

3. **Install Dependencies**

```bash
npm install
```

4. **Start the server**

```bash
npm start
```

## Noditor App

The ***Noditor App*** is a progressive web app. Enter https://github.com/wkande/noditor-app into your browser. On a mobile device consider installing the Noditor App by "Adding to Home Screen".

Use an ***Administrator Email Address*** (from the Noditor Server noditor.json file) to autheticate. You will need the address:port of your Noditor Server.

## Send a Message

After the Noditor Server is setup, connect to it with the Noditor App using a valid Adminstrator email that was added to the noditor.json file. Try this quick start to send a message from your Application.

* Using the Noditor App add a ***Key*** named *my-app-key*.

* Use the Key to send a message from your Application. This example is Node.js using Axios.

```javascript
import axios from "axios";

let res = await axios.post("https://www.yourdominan.com/alert", 
  {
    "key":"my-app-key", 
    "msg":"The server has started"
  },
  {"timeout":200}
);
console.log(res.data);
```

The message hits the Noditor Server ***POST /alert endpoint***, is stored in the SQLite3 database and is sent immediately to the Noditor App using Server Side Events.

To learn more about messaging the Noditor Server and how to send graph data jump over to the [Noditor Server](../server/messages.md?id=Messages) section of this guide and check the [API Reference](../apis/authorization?id=Authorization) as well.