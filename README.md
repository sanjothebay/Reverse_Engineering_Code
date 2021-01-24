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

 #### config.json File:

 This file is the config.json is the main configuration file. Data from config.json is used to configure virtual machine. After editing file make sure that your JSON syntax is valid. it specify global values, conditional environment and platform values, and widget dependencies.


## models <a name="models"></a>

models Folder was created by running sequelize init:models and adds a index.js file.. (sequelize cli)

![image](https://user-images.githubusercontent.com/67298961/105268254-7a798a00-5b57-11eb-9ca1-d2fe64609297.png)

#### index.js file:

index.js Grabbing all the models and putting all of the models in a DB object.
The File is being exported and being use on teh server.js to sync all the models at the same time.
Index will read in ALL of the OTHER js files in models subdirectory, and build up a db object for you. You can then use it in your api-routes for the express server.

#### user.js File:

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

Pubic Folder:
The node_modules directory is only for build tools. The package. json file in the app root defines what libraries will be installed into node_modules when you run npm install . Very often with an angular app, on your dev machine or on a build server, you use other Javascript libraries from npm.


### Folder js:

#### File login.js:

loginForm, emailInput, and passwordInput are VARIABLES referencing the html input form. 
There is event.preventDefault(); Function to prevent the page from reloding.
In the on "submit" Event. Here we are validating / Checking if there is an email and password "submit" when the "submit" button is clicked/push on. It's getting the VALUE (input by the End_User) and ().trim() is removing the whitespace from both ends of a string. (space, tab, no-break space, etc.) . It's Doing this for both the email and the password. 
If we have a correct email and password entered we then run the loginUser function.  ( Explanation on Bottom for loginUser function). 
emailInput.val("");  and  passwordInput.val(""); will Claer the Value Entered by the End-User. 
The loginUser function the POST method is called to add the resource   (to the "api/login" route the email and password). If the POST was successful (accepts the data) it will redirect the End-User to The members page, But if it catches meaning if it detects an error it will throw an error.



#### File members.js:

the GET request is retrieving data to figure out which End-User is logged in. It will then run the function to display the data in the HTML (members.html) for (".member-name").


#### File signup.js:

loginForm, emailInput, and passwordInput are VARIABLES referencing the HTML input form this is to Display the input by the End- User. 
There is event.preventDefault(); Function to prevent the page from reloding.
In the on "submit" Event for the login Form. Here we are validating / Checking if there is an email and password "submit" when the "submit" button is clicked/push on. It's getting the VALUE (input by the End_User) and ().trim() is removing the whitespace from both ends of a string. (space, tab, no-break space, etc.) . It's Doing this for both the email and the password. 
If we have a correct email and password entered we then run the loginUser function.  ( Explanation on Bottom for loginUser function). 
emailInput.val("");  and  passwordInput.val(""); will Claer the Value Entered by the End-User. 
The loginUser function the POST method is called to add the resource   (to the "api/login" route the email and password). If the POST was successful (accepts the data) it will redirect the End-User to The members page, But if it catches meaning if it detects an error it will throw an error.


![image](https://user-images.githubusercontent.com/67298961/105268833-7dc14580-5b58-11eb-907c-410b6e9b20a6.png)

##### Folder stylesheets: ....

#### File stlye.css

The css style folder is given a margin-top of 50px to both the signup  and login Form so its not all on the top and is centered a little bit with its is  It is referencing the form for the signup and login

![image](https://user-images.githubusercontent.com/67298961/105268970-b95c0f80-5b58-11eb-8e77-2d4ef02f8bf1.png)


 #### Files login.html:


#### File members.html:



#### File signup.html:

![image](https://user-images.githubusercontent.com/67298961/105269152-0213c880-5b59-11eb-9ce2-724c801146b1.png)

## routes <a name="routes"></a>

![image](https://user-images.githubusercontent.com/67298961/105269252-2ec7e000-5b59-11eb-93e6-73de8698b9be.png)

#### api-routes.js File:

Here its requiring the models and the passport Folder and its content to use in the api-routes.js. All the routes are within a function are to be exported and use with the passport.authenticate middleware to be redirected Either to continue with the request or redirect them to the login page (the Function is used by all routes ).
The .post("/api/login") If the End-User Credentials are correct it will send the End-User to the member's page. Else if the credentials are not correct it will redirects them to an error page (passport.authenticate).
The .post("/api/signup") This is the route for signing up the End-User.
It creates the required input from the End-User which is email and password. if it's successful it well, redirect the End-User to the member's page route. If it was not successful It will throw an Error.
The .get("/logout") Is the route to log out the End-User
It requires a built function logout(); and redirects the End-User to the login as per redirect("/");
The .get("/api/user_data") This the Route that is gathering Data from the End-User. Data that will be used for access. If the End-User is unsuccessful with his inputs it will send back and back an empty object error. If it's successful It will send back the inputted email by the End-User

#### html-routes.js File:

Here I am requiring the path to use the relative routes to our HTML files. Its also requiring the isAuthenticated Foder. The passport.authenticate middleware is checking if a user is logged in. All the routes are within a function are to be exported and use with the passport.authenticate middleware to be redirected Either to continue with the request or redirect them to the login page (the Function is used by all routes ).
The .get("/"); This is the route that will send the End-User to the members page. If the End-User already has an account. This route is also using the passport.authenticate middleware. (See Above). The Function us using the "../public/signup.html" File for Display.
The .get("/login"); If the End-User Credentials are correct it will send the End-User to the member's page. Else if the credentials are not correct it will redirect them to an error page (passport.authenticate). The Function us using the "../public/login.html" File for Display.
the .get("/members") is using the isAuthenticated middleware and is checking if an End-User is not logged in tries to access the members page. It will redirect them to the signup page("../public/members.html"). The Function us using the "../public/members.html" File for Display

## .gitignore <a name=".gitignore"></a>

gitignore files contain patterns that are matched against file names in your repository to determine whether or not they should be ignored. Ignoring files in Git. Git ignore patterns. Shared .gitignore files in your repository. Personal Git ignore rules.

![image](https://user-images.githubusercontent.com/67298961/105269306-469f6400-5b59-11eb-9e87-21fbd6c79ed8.png)

## package.json <a name="package.json"></a>

All npm packages contain a file, usually in the project root, called package. json - this file holds various metadata relevant to the project. This file is used to give information to npm that allows it to identify the project as well as handle the project's dependencies
A package. json is a JSON file that exists at the root of a Javascript/Node project. It holds metadata relevant to the project and it is used for managing the project's dependencies, scripts, version and a whole lot more

![image](https://user-images.githubusercontent.com/67298961/105269381-65055f80-5b59-11eb-9f1e-d337ce77671d.png)

## server.js <a name="server.js"></a>

its requiring express, express-session these are necessary npm packages to have the app fuctioning in with node. Its requiring "./config/passport" File as it been configured. Its Setting up port and requiring models for syncing with var PORT = process.env.PORT || 8080; 
its also Creating the express app and configuring middleware this is needed for authentication in the password 
Its is also requiring our routes to the HTML and the API . "./routes/html-routes.js"  "./routes/api-routes.js"  
The Server connection 
db.sequelize.sync() to sync all the models at the same time. used in index.js file. it Sync the  database and its displays a login message to the End-User.

![image](https://user-images.githubusercontent.com/67298961/105269430-85cdb500-5b59-11eb-85c5-72500ce10197.png)
