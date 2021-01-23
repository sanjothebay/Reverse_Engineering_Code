# Reverse_Engineering_Code

https://sanjothebay.github.io/Reverse_Engineering_Code/

https://github.com/sanjothebay/Reverse_Engineering_Code

# Table of contents

1. [Instruction](#Instruction)
2. [User Storie](#User_Storie)
3. [Getting Started](#Getting_Started)
4. [config](#config)
5. [models](#models)
6. [public](#public)
7. [routes](#routes)
8. [.gitignore](#.gitignore)
9. [package.json](#package.json)
10. [server.js](#server.js)

## Instruction <a name="Instruction"></a>

Reverse engineer the starter code provided and create a tutorial for the code.
Inspect the code to get a better understanding of each file's and it's responsibility.
Write a tutorial explaining every file and its purpose. If one file is dependant on other files, be sure to let the user know.

## User Storie <a name="User_Storie"></a>

```
AS A developer

I WANT a walk-through of the codebase

SO THAT I can use it as a starting point for a new project

```

## Getting Started <a name="Getting_Started"></a>

#### Directory structure

All the recommended files and directories structure:

```

┌────── config
│   │   └── middleware
│   │       └── isAuthentication.js
│   ├── config.json
│   └── passport.js
│ 
├── models
│   ├── index.js
│   └── user.js
│ 
├── node_modules
│ 
│
├─────────── public
│    │     │  └── js
│    │     │      ├── login.js
│    │     │      ├── members.js
│    │     │      └── signup.js
│    │     │
│    │     └── stylesheets
│    │         └── style.css
│    ├── login.html
│    ├── members.html
│    └── signup.html
│
├─── routes
│    ├── api-routes.js
│    └── html-routes.js
│
├── .gitignore
│
├── package-lock.json
│
├── package.json
│
├── server.js
│
├── README.md
│
└── server.js

```

## config <a name="config"></a>

config Folder was created by running sequelize init:config and adds a config.json file.. (sequelize cli)

![image](https://user-images.githubusercontent.com/67298961/105268545-0db2bf80-5b58-11eb-9433-41b409a2ae28.png)
 
 middleware Folder File isAuthenticate.js:
 the passport.authenticate middleware redirected Either to continue with the request or redirect them to the login page (the Function is used by all routes ). More details with [routes](#routes) . 

 config.json File:
 This file is the config.json is the main configuration file. Data from config.json is used to configure virtual machine. After editing file make sure that your JSON syntax is valid. it specify global values, conditional environment and platform values, and widget dependencies.


## models <a name="models"></a>

models Folder was created by running sequelize init:models and adds a index.js file.. (sequelize cli)

![image](https://user-images.githubusercontent.com/67298961/105268254-7a798a00-5b57-11eb-9ca1-d2fe64609297.png)

index.js file:
index.js Grabbing all the models and putting all of the models in a DB object.
The File is being exported and being use on teh server.js to sync all the models at the same time.
Index will read in ALL of the OTHER js files in models subdirectory, and build up a db object for you. You can then use it in your api-routes for the express server.

user.js File:
Its Requiring bcrypt for the password for the transformation of a string of characters used to index and retrieve items in a database. it's a secured way to store passwords in my database

It's exporting the module Function that is within the table being created.
The table that is being created is saved in a variable called User the Table is being created by sequelize syntax.

email is a VALUES being created. it's a DataTypes.STRING, (VARIABLE). the email cannot be Null (empty). It's using unique to enforce the uniqueness rule to ensures values in a column. it contains a validate to check the email and it set to true.
password is another VALUES being created. it's a DataTypes.STRING,
the password cannot be Null (empty).

User.prototype.validPassword is the custom method for the End-User model. It will check if an unbcryptjs password entered by the user can be compared to the bcryptjs password stored in our database

User.addHook("beforeCreate")
these are methods that run during the various phases of the User Model lifecycle of the End- User using the application. Before a member is created, it will automatically bcryptjs their password.

## public <a name="public"></a>

Folder js

![image](https://user-images.githubusercontent.com/67298961/105268833-7dc14580-5b58-11eb-907c-410b6e9b20a6.png)

Folder stylesheets

![image](https://user-images.githubusercontent.com/67298961/105268970-b95c0f80-5b58-11eb-8e77-2d4ef02f8bf1.png)

Files .html

![image](https://user-images.githubusercontent.com/67298961/105269152-0213c880-5b59-11eb-9ce2-724c801146b1.png)

## routes <a name="routes"></a>

![image](https://user-images.githubusercontent.com/67298961/105269252-2ec7e000-5b59-11eb-93e6-73de8698b9be.png)

api-routes.js File:
Here its requiring the models and the passport Folder and its content to use in the api-routes.js. All the routes are within a function are to be exported and use with the passport.authenticate middleware to be redirected Either to continue with the request or redirect them to the login page (the Function is used by all routes ).

The .post("/api/login") If the End-User Credentials are correct it will send the End-User to the member's page. Else if the credentials are not correct it will redirects them to an error page (passport.authenticate).

The .post("/api/signup") This is the route for signing up the End-User.
It creates the required input from the End-User which is email and password. if it's successful it well, redirect the End-User to the member's page route. If it was not successful It will throw an Error

The .get("/logout") Is the route to log out the End-User
It requires a built function logout(); and redirects the End-User to the login as per redirect("/");

The .get("/api/user_data") This the Route that is gathering Data from the End-User. Data that will be used for access. If the End-User is unsuccessful with his inputs it will send back and back an empty object error. If it's successful It will send back the inputted email by the End-User

html-routes.js File:
Here I am requiring the path to use the relative routes to our HTML files. Its also requiring the isAuthenticated Foder. The passport.authenticate middleware is checking if a user is logged in. All the routes are within a function are to be exported and use with the passport.authenticate middleware to be redirected Either to continue with the request or redirect them to the login page (the Function is used by all routes ).

The .get("/"); This is the route that will send the End-User to the members page. If the End-User already has an account. This route is also using the passport.authenticate middleware. (See Above). The Function us using the "../public/signup.html" File for Display

The .get("/login"); If the End-User Credentials are correct it will send the End-User to the member's page. Else if the credentials are not correct it will redirect them to an error page (passport.authenticate). The Function us using the "../public/login.html" File for Display

the .get("/members") is using the isAuthenticated middleware and is checking if an End-User is not logged in tries to access the members page. It will redirect them to the signup page("../public/members.html"). The Function us using the "../public/members.html" File for Display

## .gitignore <a name=".gitignore"></a>

![image](https://user-images.githubusercontent.com/67298961/105269306-469f6400-5b59-11eb-9e87-21fbd6c79ed8.png)

## package.json <a name="package.json"></a>

![image](https://user-images.githubusercontent.com/67298961/105269381-65055f80-5b59-11eb-9f1e-d337ce77671d.png)

## server.js <a name="server.js"></a>

![image](https://user-images.githubusercontent.com/67298961/105269430-85cdb500-5b59-11eb-85c5-72500ce10197.png)
