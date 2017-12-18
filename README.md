# Stateless-vs-stateful-authentication


![pic1](https://cdn.auth0.com/blog/cookies-vs-tokens/cookie-token-auth.png)


# Cookie Based Authentication

#### Cookie based authentication has been the default, tried-and-true method for handling user authentication for a long time.

#### Cookie based authentication is stateful. This means that an authentication record or session must be kept both server and client-side. The server needs to keep track of active sessions in a database, while on the front-end a cookie is created that holds a session identifier, thus the name cookie based authentication. Let's look at the flow of traditional cookie based authentication:

    1- User enters their login credentials
    2- Server verifies the credentials are correct and creates a session which is then stored in a database
    3- A cookie with the session ID is placed in the users browser
    4- On subsequent requests, the session ID is verified against the database and if valid the request processed
    5- Once a user logs out of the app, the session is destroyed both client and server side
