# ![EJS - Setup](./assets/hero.png)


Open your Terminal application and navigate to your `~/code/ga/lectures` directory:

```bash
cd ~/code/ga/lectures
```

Make a new directory called `ejs`, then enter this directory:

```bash
mkdir ejs
cd ejs
```

Then, create a `server.js` file. This file will hold your work for this lecture:

```bash
touch server.js
```

With the file created, open the contents of the directory in VS Code:

```bash
code .
```

In the terminal, create a `package.json` with all of the default settings by running the following command:

```bash
npm init -y
```

Open the new `package.json` file, and add the following line below `"description": "",` to let `node` know that our project is using ES modules: 

```bash
"type": "module",
```

Now that we have a `package.json` file we can add a package from `npm` to our project. We're going to add `Express` to our project next: 

```bash
npm i express
```

> 🧠 The i in npm i is an alias for install


In `server.js`, add the following starter code: 

```javascript
import express from 'express'
const app = express()

app.get('/', (req, res) => {
  res.send('Server is running')
})

app.listen(3000, () => {
  console.log('Listening on port 3000')
})
```

- Use `node` to execute the `server.js` file by using this command in your terminal:

```bash
node server.js
```

[tktk - do we prefer npm start here? Do we prefer nodemon if we can verify it was globally installed?]



