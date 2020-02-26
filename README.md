# GitHub OAuth Login example

This is an example web app which uses your OAuth app for authentication.

Here is a description about the OAuth [Web application flow](https://developer.github.com/apps/building-oauth-apps/authorizing-oauth-apps/#web-application-flow).

## Setup

1. Serve the index.html over http(s)
2. Create a new OAuth app
3. Deploy an OAuth server
4. Adapt index.html

### Step 1: Serve the index.html over http(s)

Clone the repository (or alternatively download the ZIP file)

```
git clone https://github.com/gr2m/github-oauth-login.git
cd github-oauth-login
```

Start a server in the current folder. For example, if you have python installed, you can just run

```
python -m SimpleHTTPServer
```

This will start a server at `http://localhost:8000`.

### Step 2: Create a new OAuth app

You can create an OAuth app [with your account](https://github.com/settings/applications/new) or with a GitHub organization. Give the app a name and a homepage (neither matter). Set the **Authorization callback URL** to the URL from step 1, e.g. `http://localhost:8000`.

### Step 3: Deploy an OAuth server

You need to deploy a small server which keeps the OAuth app’s secret safe, as it cannot be shared in the browser.

The simplest way to do that is [@HenrikJoreteg](https://github.com/HenrikJoreteg)’s [github-secret-keeper](https://github.com/HenrikJoreteg/github-secret-keeper). You can deploy it easily to https://glitch.com/. Press on "New Project" on the top right, then press the "Clone from Git Repo" button and paste in `https://github.com/HenrikJoreteg/github-secret-keeper.git`

After the project is imported, edit the `package.json` file and add

```json
  "scripts": {
    "start": "node server.js"
  }
```

Then create a new file called `.env` and enter the following

```
<client id>=<client secret>
```

Replace `<client id>` with your OAuth app’s clientid, and the same with `<client secret>`. At the end it will look something like this

```
af35402964c3be2ada1c=3a919e462c79397ebf89dbe0338e112d25e94c1c
```

### 4. Adapt index.html

Finally, edit the `index.html`.

Replace `const CLIENT_ID = "af3540296c43be2ada1c";` with your app’s client ID. Replace `https://henrikjoreteg-github-secret-keeper.glitch.me/:client_id/:code` with your Glitch app’s URL.

## License

[ISC](LICENSE)
