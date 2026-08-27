Tags: [[_JavaScript]] [[__Programming_languages]]
#JavaScript #ProgrammingLanguages 

# Introduction
Passport.js is an authentication middleware framework for Express. Its main job is to take an incoming request, figure out who the user is and then make that user available as `req.user`:
```javascript
router.get('/:id/columns', checkAuthenticated, async (req, res) => {
	req.user // User which makes the request
	
// check if user is authenticated (if he has logged in)
function checkAuthenticated(req, res, next) {
    if (req.isAuthenticated()) {
        return next()
    }

    return res.redirect('/login')
}
```
# Strategies
A strategy defines how authentication happens.

For example, Passport has a `LocalStrategy` for username/password authentication.

You might configure it roughly like:
```javascript
passport.use(new LocalStrategy(
    async (username, password, done) => {
        const user = await usersDocs.findOne({
            email: username
        })

        if (!user) {
            return done(null, false)
        }

        // check password...
        
        return done(null, user)
    }
))
```

This part:
```javascript
return done(null, user)
```
tells Passport: "I successfully authenticated this request. This is the user."

And this:
```javascript
return done(null, false)
```
means "Authentication failed."
# Sessions
Sessions are used so that a user doesn't have to log in every time they want to make a request to the app.

It works like this:
- When a user gets authenticated, a session is created for them and session ID is stored in cookie. 
- That session contains information about the user which is then used to find this user
	- We use serialization and deserialization to define what information is stored and how it is used to find the user
- Then, when a user makes a request, instead of logging in again, the session ID is retrieved from cookie to determine that his user is already authenticated.
## Serialization and deserialization
Serialization defines what information about the user is stored when creating a session. For example, this code specifies to store user's ID:
```javascript
passport.serializeUser((user, done) => {
    done(null, user.id)
})
```

Deserialization defines how to find a user in a database based on the information about the user stored in a session defined by the serialization, for example based on user ID:
```javascript
passport.deserializeUser(async (id, done) => {
    const user = await usersDocs.findById(id)

    done(null, user)
})
```
# Request attributes and methods provided by the Passport
Request attributes provided by the Passport:
- `user`

And methods:
- `isAuthenticated`

We can access them like this:
```javascript
router.get('/:id/columns', checkAuthenticated, async (req, res) => {
	req.user // User which makes the request
	req.isAuthenticated // Check whether the user is authenticated (true or false)
```
# Authenticating a user
We authenticate a user:
- For the first time when they log in
- Every time they make a request

Every time a user makes a request, we check whether they have already logged in and are authenticated.

Both those authentications are done in a different way described below.
## Authentication when logging in - `passport.authenticate()`
To authenticate a user when logging in (to verify a username and a password), we use the `passport.authenticate()` function:
```javascript
router.post(
    '/login',
    passport.authenticate('local', {
        failureRedirect: '/login',
        failureFlash: true
    }),
    (req, res) => {
        res.redirect('/')
    }
)
```

The `passport.authenticate()` function calls then the authentication function which we define in the local strategy.

We define to use a local strategy like this:
```javascript
passport.use(new localStrategy(
	{
		usernameField: 'email',
		passwordField: 'password' // This is the default value, we can skip this
	}
	,authenticateUser
))
```

and this specifies to:
- Use the `authenticateUser` function for authentication
- Take the following parameters for this function:
	- username from the `req.body.email` field
	- password from the `req.body.password` field

So authentication will be done by calling the following function with the following arguments:
```javascript
authenticateUser(email, password, done)
```

The `done` argument is provided by Passport (we don't specify it). It is used as a variable which the authentication function returns:
- `done(null, user)` - means that authentication succeeded
- `done(null, false, info)` - means that authentication failed`

And this function can looks for example like this:
```javascript
const authenticateUser = async (email, password, done) => {
	const user = await getUserByEmail(email)
	if (user == null){
		// below message will be accessible in ejs file as messages.error variable
		return done(null, false, {message: 'No user with that email'})
	}

	try {
		if (await bcrypt.compare(password, user.password)){
			return done(null, user)
		} else {
			return done(null, false, {message: 'Password incorrect'})
		}
	} catch(e) {
		return done(e)
	}
}
```
## Authentication when making a request - `isAuthenticated` and `checkAuthenticated`
We can use the `isAuthenticated()` request's method and create the `checkAuthenticated` function to check whether a user is authenticated when making a request, i.e. whether that user has already logged in.

The `isAuthenticated()` request's method uses data from a session to verify whether a user is authenticated.

The `isAuthenticated()` method for the request object returns true or false and indicates whether the user making the request is authenticated:
```javascript
router.get('/:id/columns', async (req, res) => {
	// Check whether the user is authenticated (returns true or false)
	req.isAuthenticated() 
```

We can use this method to create the `checkAuthenticated` function which will be used to verify whether a user is already logged in every time they make a request.

We can define a function like this:
```javascript
function checkAuthenticated(req, res, next) {
    if (req.isAuthenticated()) {
        return next()
    }

    res.status(401).send('Not authenticated')
}
```

and use it when handling a request:
```javascript
router.get(
    '/:id/table',
    checkAuthenticated,
    async (req, res) => {
        ...
    }
)
```