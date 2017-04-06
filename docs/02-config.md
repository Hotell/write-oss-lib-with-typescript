## Setting up Github

- Log in to GitHub
- Create a repository with a name `starwars-ts-names-{NAME}`
  - **NOTE:** that {NAME} is a placeholder for your name/github-account-name
- Clone that repo to your HDD `git clone https://github.com/{YOUR GITHUB ACCOUNT}/starwars-ts-names-{NAME}`
- `cd starwars-ts-names-{NAME}`


## Configure NPM

Repeating itself is error prone and not very effective right?

Let's setup our npm package manager so we don't have to bother next time we will use it:

```bash
npm set init-author-name ‘Your Name’

npm set init-author-email ‘your@email.com’

npm set init-author-url ‘http://your-web.com’ - optional

npm set init-license ‘MIT’

npm set save-exact true
```

Now check if everything was setup correctly.

```bash
npm config list
```

you should see output similiar to this:

```bash
> $ npm config list

init-author-email = "hochelmartin@gmail.com"
init-author-name = "Martin Hochel"
init-license = "MIT"
save-exact = true
```


## Login to NPM on your PC

```bash
npm adduser
```

- use your email
- use npm name that you registered
- enter you password

DONE!

now you are able to publish packages to npm




