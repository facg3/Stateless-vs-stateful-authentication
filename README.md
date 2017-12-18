# Stateless-vs-stateful-authentication


## 1- In Session-based Authentication (Stateful)

### the Server does all the heavy lifting server-side. Broadly speaking a client authenticates with its credentials and receives a session_id (which can be stored in a cookie) and attaches this to every subsequent outgoing request. So this could be considered a "token" as it is the equivalent of a set of credentials. There is however nothing fancy about this session_id-String. It is just an identifier and the server does everything else. It is stateful. It associates the identifier with a user account (e.g. in memory or in a database). It can restrict or limit this session to certain operations or a certain time period and can invalidate it if there are security concern and more importantly it can do and change all of this on the fly. Furthermore it can log the users every move on the website(s). Possible disadvantages are bad scale-ability (especially over more than one server farm) and extensive memory usage.


## 2- In Token-based Authentication (Stateless)
### no session is persisted server-side (stateless). The initial steps are the same. Credentials are exchanged against a token which is then attached to every subsequent request (It can also be stored in a cookie). However for the purpose of decreasing memory usage, easy scale-ability and total flexibility (tokens can be exchanged with another client) a string with all the necessary information is issued (the token) which is checked after each request made by the client to the server.
