# Stateless vs stateful authentication
- Authentication used to be stateful for a long period of time. This means that the users used to input their entries. Then the server creates an id session, store it server-side

- All user data used to be stored server-side.

- Any service that uses user data must consult the data store first.

- This used to be somewhat good because if the data is centralized, user data will less likely be fudged.

- But this generated a problem for complex architecture because needing to consult the data store for every operation is troublesome. Thus, the idea of Stateless authentication emerged.


![pic1](https://cdn.auth0.com/blog/cookies-vs-tokens/cookie-token-auth.png)


# Cookie/Session Based Authentication(stateful)

#### Cookie based authentication has been the default, tried-and-true method for handling user authentication for a long time.

#### Cookie based authentication is stateful. This means that an authentication record or session must be kept both server and client-side. The server needs to keep track of active sessions in a database, while on the front-end a cookie is created that holds a session identifier, thus the name cookie based authentication. Let's look at the flow of traditional cookie based authentication:

    1- User enters their login credentials
    2- Server verifies the credentials are correct and creates a session which is then stored in a database
    3- A cookie with the session ID is placed in the users browser
    4- On subsequent requests, the session ID is verified against the database and if valid the request processed
    5- Once a user logs out of the app, the session is destroyed both client and server side

#  Token-Based Authentication

#### Token-based authentication is stateless. The server does not keep a record of which users are logged in or which JWTs have been issued. Instead, every request to the server is accompanied by a token which the server uses to verify the authenticity of the request. The token is generally sent as an addition Authorization header in form of Bearer {JWT}, but can additionally be sent in the body of a POST request or even as a query parameter. Let's see how this flow works:


    1- User enters their login credentials
    2- Server verifies the credentials are correct and returns a signed token
    3- This token is stored client-side, most commonly in local storage - but can be stored in session storage
    or acookie as well
    4- Subsequent requests to the server include this token as an additional Authorization header or through
    one of the other methods mentioned above
    5- The server decodes the JWT and if the token is valid processes the request
    6- Once a user logs out, the token is destroyed client-side, no interaction with the server is necessary.
    
   ## Stateless advantages:

**1.Reduces memory usage** Image if google stored session information about every one of their users.

**2.Easier to support server farms** If you need session data and you have more than 1 server, you need a way to sync that session data across servers. Normally this is done using a database.

**3.Reduce session expiration problems** Sometimes expiring sessions cause issues that are hard to find and test for. Sessionless applications don't suffer from these.

**4.Url linkability** Some sites store the ID of what the user is looking at in the sessions. This makes it impossible for users to simply copy and paste the URL or send it to friends.

## Stateless disadvantages:

**1.Compromised Secret Key**: The best and the worst thing about JWT is that it relies on just one Key. Consider that the Key is leaked by a careless or a rogue developer/administrator, the whole system is compromised!

**2.Cannot manage client from the server:** We had several cases where we wanted the users at HelpTap to logout by cleaning up the cookies, but we cannot ask them to do so every time. As well consider the case that a user’s mobile is stolen, and he wants to logout of all existing sessions(e.g. Gmail’s logout other sessions feature). Well its not possible in case of JWT.

**3.Cannot push Messages to clients (Identifying clients from server) :** As we have no record about the logged-in clients on the DB end, we cannot push messages to all the clients.

**4.Crypto-algo can be deprecated:** JWT relies completely on the Signing algorithm. Now, though it is not frequent, but in the past many Encryption/Signing algorithms have been deprecated.

**5.Data Overhead:** The size of the JWT token will be more than that of a normal Session token. The more data you add in the JWT token, the longer it gets linearly.

**6.Complicated to understand:** JWT uses cryptographic Signature algorithms to verify the data and get the user-id from the token. Understanding the Signing Algo in itself requires basics of cryptography. So, in case if the developer is not completely educated s/he might introduce security loopholes in the system.
