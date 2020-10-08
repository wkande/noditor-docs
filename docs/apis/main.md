# API Reference

REST API Endpoints served by the Noditor Server.

[filename](auth.md ':include')


## Keys

***Keys*** are only used when sending a message or graph data from your Application to the Noditor Server.

- POST /alert
- POST /error
- POST /graph

You create Keys using the Noditor App. Generally, you will create a Key for each instance of a backend application and a single Key for a frontend application.

Keys provide two important functions.

- Group data into a logical bucket.
- Provides security for the API call, Keys are a secret.

Learn more about [Keys](server/config.md?id=keys) in the API Reference section of this guide.

[filename](keys/keys-get.md ':include')

[filename](keys/key-create.md ':include')

[filename](keys/key-delete.md ':include')

## Users

***Users*** are allowed access to the Noditor App. Administrators create users using the Noditor App. When accessing the Noditor App a user must go through the email-code-token challenge.

[filename](users/code-post.md ':include')

[filename](users/token-get.md ':include')
