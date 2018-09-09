# Description

I created this repository to help debug an issue I reported on [StackOverflow](https://stackoverflow.com/questions/52235245/then-method-is-not-executing-in-nodejs). The issue I'm having is that the `.then()` method is not being executed when I call the mongoose `findOne()` method, which seems not to be returning a es2015 `Promise`. More details of the issue can be found on the [StackOverflow Question](https://stackoverflow.com/questions/52235245/then-method-is-not-executing-in-nodejs).

# Requirments

node v8.11.1
MongoDB shell version v4.0.1
MongoDB server version: 4.0.1

# Installation

To reproduce this issue you need to first install and setup MongoDB and then Node.js app of this repository.

## Install MongoDB

1. Install the MOngoDB community server from their [download centre](https://www.mongodb.com/download-center#community).
2. Launch the MongoDB server with the `mongod` command in your terminal. _(You can stop it by pressing CTRL + C)_
3. IN a new terminal window connect to the MongoDB via it's `mongo` shell command.
4. Create a database with following commands...
   `use devconnector`
   `db.testData.insert( { Description : "Initial document used to create database" } )`

## Install Nodejs app from this Repository

Follow

```bash
git clone https://github.com/bradtraversy/devconnector.git
cd devconnector
npm install
npm run debug
```

# Reproducing the issue

Open your browser at http://localhost:5000/ and in it's console enter...

```js
fetch("http://localhost:5000/api/users/register", {
  method: "POST",
  body: JSON.stringify({
    name: "holly",
    email: "holly@mail.com",
    password: "holly123"
  }),
  headers: {
    "Content-type": "application/json; charset=UTF-8"
  }
})
  .then(response => response.json())
  .then(json => console.log(json));
```

If you use the nodeJS debugger you will see that the code does not execute line 29 of routes/api/users.js.
