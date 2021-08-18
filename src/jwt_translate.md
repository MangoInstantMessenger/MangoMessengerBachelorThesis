# About tokens, JSON Web Tokens, authentication and authorization. Token-Based authentication

- What is authorization/authentication
- Where to store tokens
- How to set cookies
- Login process
- Refresh token process
- Theft of tokens/Token control mechanism
- JWT vs Cookie sessions

## Base

**Authentication(from the Greek. αὐθεντικός [authentikos] - real, genuine; by αὐθέντης [authentes] - author)** - it is process which verify user credentials (login and password)
User authentication by comparing the login and password entered by him with the data saved in the database.

**Authorization** - it is process which check of the user's rights to access certain resources.

For example, after authentication the user **Bob** gets the right to access and get from resource "**super.com/vip**" some data.
When the user **Bob** accesses to the vip resource, the authorization system will check has the user right to access this resource. 

1. The user with email **bob@gmail.com** successfully authenticated.
2. The server checks in database role of **Bob**.
3. The server generated token with specified role.
4. **Bob** go in a certain resource using received token.
5. The server check user rights in token and respectively skips or cuts the request.

The fifth point is the authorization.

JSON Web Token (JWT) -- contains 3 blocks separated by dots: **header**, **payload** and the **signature**. 
The first 2 blocks presented in JSON-format and additionally encoded to the format base64.
Payload contains arbitary key-value pairs.
The JWT standard defines several reserved names (iss, aud, exp, and others).
Signature can be generated with help of symmetric and asymetric encryption algorithms.
In addition, there is a separate standard that describes the format of the encrypted JWT-token.

Example of JWT-token with encrypted 1st and 2nd blocks: 

```
{ alg: "HS256", typ: "JWT" }.{ iss: "auth.myservice.com", aud: "myservice.com", exp: 1435937883, userName: "Bob", userRole: "Admin" }.S9Zs/8/uEGGTVVtLggFTizCsMtwOJnRhjaQ2BMUQhcY
```

Tokens presents a means of authorization for every request from client to server.
Tokens are generatedon the server based on secret key which stored in the server and payload.
As a result, token stored on the client and used when it is necessary to authorize any requests.

When a hacker tries to replace the data in the **header** or **payload**, token will become invalid, since the **signature** will not match the original values.
And the hacker does not ability to generate a new signature, since the encryption secret key stored in the server.

**accessToken** - used for request authorization and for storing the additionally information about user (**userId**, **displayName** and others, this information is also called **payload**).
All **payload** fields is free set of fields necessary for implementation your private business logic.
That is **userId** and **displayName** is not required fields and presents only a special case.
**Access and refresh tokens store in the local storage**

**refreshToken** - issued by server based on successful authentication results and used for get new access/refresh token pair.

Every token has its own lifetime. For example: **accessToken**: 5 minute, **refreshToken**: 7 minute

Since tokens are not encrypted information, it is highly not recomended to store any sensitive data in them (password hashes, payment credentials, etc ...)

## How to set cookies?
In order to **refreshToken** cookie was setted successfully and sended from the browser,
endpoint addresses of authentication(`api/session` - login, `api/session/{Id}` - refresh token, `api/session/{Id}` - logout) should be locate in domain environment of the site.
That is, for `super.com` we are set the cookie with such options:

```cookie
{
    domain: '.super.com',
    path: '/api/session'
}
```

Thus, the cookie will be installed in the browser and will come to all endpoints at `super.com/api/session/<any-path>`

If you have a monolith and the same API is responsible for authentication, there should be no problems here.
But if a separate microservice is responsible for authentication, we hide it using nginx using the above path (`super.com/api/auth`).

## Create session/tokens, login 

1. The user logs into the application by transferring the login/password and fingerprint of the browser (well, or some other unique device identifier if it is not a browser).
2. The server verifies the authenticity of the username/password.
3. If successful, creates and writes a session to the database {`UserId: uuid, RefreshToken: uuid, ExpiresIn: int, Fingerprint: string, ...`} (table schema below).

```sql
CREATE TABLE refreshSessions (
    "Id" SERIAL PRIMARY KEY,
    "UserId" uuid REFERENCES users(id) ON DELETE CASCADE,
    "RefreshToken" uuid NOT NULL,
    "UserAgent" character varying(200) NOT NULL,
    "FingerPrint" character varying(200) NOT NULL,
    "Ip" character varying(15) NOT NULL,
    "ExpiresIn" bigint NOT NULL,
    "CreatedAt" timestamp with time zone NOT NULL DEFAULT now()
);
```

4. The server creates **access token**.
5. Sends to client **access and refresh tokens (uuid)**.

```cookie
Set-Cookie: refreshToken='c84f18a2-c6c7-4850-be15-93f9cbaef3b3'; HttpOnly // для браузера
{
  body: { 
    accessToken: 'eyJhbGciOiJIUzUxMiIsI...',
    refreshToken: 'c84f18a2-c6c7-4850-be15-93f9cbaef3b3' // for mobile applications
  }
}
```

6. Client saves **access and refresh tokens** in the local storage.

Before each request client preliminarily checks **access token** lifetime and if it expired, client sends request for updating **access token**.
For more confidence, we can update tokens a few seconds earlier.
That is, the case when the API receives an expired access token is practically excluded.

What is **finger print**? This is browser tracking tool regardless of desire of user to be identified.
This is hash generated from java script based of a certain unique parameters/components of browser
The **finger print's** advantage is that he nowhere persistently not stored and generating on login/refresh tokens moment.

Hashing library: https://github.com/Valve/fingerprintjs2

To use the authentication feature on more than one device, it is necessary to store all refresh tokens for each user. 
I store this list in a PostgreSQL table. 
During each login, a record is created with IP / Fingerprint and other meta information, the so-called refresh session (table schema above).

1. Client before each request checks **access token** lifetime.
2. If it expired, client sends `POST api/session/{Id}` `{ fingerprint: string }` to the `body` and respectively `refreshToken` cookie.
3. The server receives a record of the refresh session by the UUID of the refresh token.
4. The server saves current refresh session in the local storage and delete it from the table.
5. Checks current refresh session:
  1. Has token lifetime expired.
  2. To match the old fingerprint received from the current refresh session with the new one received from the request body.
6. In case of a negative result, throws an error `TOKEN_EXPIRED` or `INVALID_REFRESH_SESSION`.
7. If successful, it creates a new refresh session and writes it to the database.
8. The server creates **access token**.
9. Sends to client **access and refresh token (uuid)** .

```cookies
Set-Cookie: refreshToken='c84f18a2-c6c7-4850-be15-93f9cbaef3b3'; HttpOnly // для браузера
{
  body: { 
    accessToken: 'eyJhbGciOiJIUzUxMiIsI...',
    refreshToken: 'c84f18a2-c6c7-4850-be15-93f9cbaef3b3' // для мобильных приложений
  }
}
```
## Key moment:
At the time of the refresh, that is, updates to the **access token**, **BOTH** tokens are updated.
But how can a **refresh token** update itself, since it is created only after successful authentication? 
The **refresh token** at the time of the refresh compares itself with the **refresh token** that is in the database and in case of success, 
and also if it has not expired, the system refreshes the tokens.

## In case of theft of access token and refresh cookies:
1. Hacker used **access token**.
2. **Access token's** lifetime has run out.
3. **Hacker's client** sends **refresh token** and fingerprint.
4. The server is checking at the hacker's **fingerprint**.
5. The server does not find the hacker's **fingerprint** in the refresh session and deletes it from the database.
6. The server logs an attempt to update unauthorized tokens.
7. The server redirects the hacker to the login page. Hacker walks through the forest.
8. The user tries to log into the server >> it is found that there is no **refresh token**.
9. The user tries to log into the server >> it is found that there is no refresh token.
10. User enters login/password

## JWT vs Cookie sessions
Why all this hemorrhoids? Why not use the good old cookie sessions? What's wrong with cookies?

- Cookie subject to CSRF: https://owasp.org/www-community/attacks/csrf
- It is more convenient for native applications for smartphones to work with tokens. Yes, there are hacks for working with cookies, but this is not native support.
- Cookies are not an option in microservice architecture. 
Let remind you that microservices are often scattered on different domains, and cookies do not support cross-domain requests.
- In the microservices architecture, JWT allows each service, regardless of the authorization server, to verify the **access token** (via a public key).
- When using jwt, we see a security problem and try to provide control mechanisms in the event of a load of authorization data.
When using cookies, the programmer often does not even think that the session can be compromised.
- On every request, using JWT saves the backend from one request to the database (or cache) for user data (userId, email, etc.)

## Eventually
- Theft control mechanisms sensitive data in stock
- Took the best of both technologies, as much as possible secured against CSRF / XSS
- Add CSP header `SameSite=Strict` for cookie and wait the villains