---
alias: Auth
---

## Concepts

- https://www.youtube.com/watch?v=mL8EuL7jSbg
- https://www.fronttoback.dev/articles
- [Auth for Frontend Devs with Chance Strickland | JS Drops - YouTube](https://www.youtube.com/watch?v=6a8_9FdGYt4)

- What does the flow of auth look like?
    - In General
    - In SPAs
- Client vs. Server
- Authentication vs Authorization
- Passwords
- Session-based Auth
    - Unlike with token-based authentication, state is handled on the server.

```js
const express = require('express'); 
const session = require('express-session'); 

const app = express(); 

app.use(session({ 
    secret: 'secret-key',
    cookie: {
        maxAge: 1000 * 60 * 60 * 24 // 24 hours
    },
    resave: true,
    saveUninitialized: false,
}));

app.get('/', (req, res) => {
    if (!req.session.userid) {
        return res.redirect('/login');
    }

    res.setHeader('Content-Type', 'text/html')
    res.write(`
        <h1>Welcome back ${req.session.userid}</h1>
        <a href="/logout">Logout</a>
    `);

    res.end()
});

app.get('/login', (req, res) {
    if (req.session.userid) {
        return res.redirect('/');
    }
    
    res.setHeader('Content-Type', 'text/html')
    res.write(`
        <h1>Login</h1>
        <form method="post" action="/process-login">
            <input type="text" name="username" placeholder="Username" /> <br>
            <input type="password" name="password" placeholder="Password" /> <br>
            <button type="submit">Login</button>
        </form>
    `);
    
    res.end();
});

app.post('/login', loginController);

app.get('/logout', (req, res) => {
    req.session.destroy();
    res.redirect('/');
});
```

- Token-based Auth
    - Unlike with session-based authentication, tokens are managed on the client.
    - JWTs
- OAuth
- SSO
- Sessions vs. Cookies
    - Security
- Basic Auth
- OpenID
- SAML
- Authentication vs. Authorization
- Passwordless Auth
    - Passkeys
        - https://www.smashingmagazine.com/2023/10/passkeys-explainer-future-password-less-authentication/

## Bookmarks

- [JWTs vs. sessions: which authentication approach is right for you? - Stytch](https://stytch.com/blog/jwts-vs-sessions-which-is-right-for-you/)

---

## Further
### Ecosystem 🏵

- Auth.js
- Auth0
- Clerk
- [Lucia](https://lucia-auth.com/)
- Passport.js
- Supabase Auth

### Learn 🧠

- [Auth Series (YouTube)](https://youtube.com/playlist?list=PLkZYeFmDuaN2pZOuMWjIfvZ6v2ZFp2jyK)

- [The Copenhagen Book](https://thecopenhagenbook.com/)

### Reads 📄

- [How to Secure the Web: A Comprehensive Guide to Authentication Strategies for Developers (DEV)](https://dev.to/ma7moud3bas/how-to-secure-the-web-a-comprehensive-guide-to-authentication-strategies-for-developers-48od)

- [REST API Authentication Methods](https://blog.bytebytego.com/i/140010110/rest-api-authentication-methods)

### Resources 🧩

- [The Copenhagen Book](https://thecopenhagenbook.com/)

### Videos 🎥

![Session vs Token Authentication in 100 Seconds (YouTube)](https://www.youtube.com/watch?v=UBUNrFtufWo)