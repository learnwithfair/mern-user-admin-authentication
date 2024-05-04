# MERN-USER-ADMIN-AUTHENTICATION

[![Youtube][youtube-shield]][youtube-url]
[![Facebook][facebook-shield]][facebook-url]
[![Instagram][instagram-shield]][instagram-url]
[![LinkedIn][linkedin-shield]][linkedin-url]

Thanks for visiting my GitHub account!

<img src ="https://cdn-icons-png.flaticon.com/512/1791/1791961.png" height = "200px" width = "200px"/>**Authentication** is the process of determining whether someone or something is who or what they say they are. Authentication technology provides access control for systems by checking to see if a user's credentials match the credentials in a database of authorized users or a data authentication server. In doing this, authentication ensures that systems, processes and enterprise information are secure.

There are several authentication types. For user identity, users are typically identified with a user ID; authentication occurs when the user provides credentials, such as a password, that match their user ID.

**Web Authentication** is a web standard published by the World Wide Web Consortium. WebAuthn is a core component of the FIDO2 Project under the guidance of the FIDO Alliance[see-more](https://www.techtarget.com/searchsecurity/definition/authentication)

## Source Code (Download)

- [Source-code]()
- [Documentation](https://github.com/learnwithfair/node-express-documentation)

## Template includes

- User/Admin Registration Process
- Login with Manually/Facebook
- Login with Manually/Google.
- Verify using JWT Token
- For verification Send Mail to the user Email.
- Crud Operation
  - POST / -> search the blog (Admin/User)
  - POST /search-blogs -> search the blog (Admin/User)
  - GET /:id -> get single blog
  - POST / -> create a blog (Admin)
  - DELETE /:id -> delete a blog (Admin)
  - PUT /:id -> update a blog (Admin)

## Required Software (Download)

- VS Code, Download ->https://code.visualstudio.com/download
- Node, Download-> https://nodejs.org/en/download
- MongoDB Shell(msi) , Download-> https://www.mongodb.com/try/download/shell
- MongoDB Compass (msi), Download-> https://www.mongodb.com/try/download/community
- Postman, Download-> https://www.postman.com/downloads/

**Or Online Database (MongoDB Atlas)**

- Register -> https://www.mongodb.com/cloud/atlas/register

## ========== Environment Setup ==========

1. Install Node.js
2. To verify installation into command form by node -v
3. For initialization npm write the query in the command window as npm init -y
4. Setup the opening file into the package.json and change the file with main:'server.js'
5. To create a server using the express package then write a query into the command window as npm install express.
   Write code in the server file for initialization
   const express = require("express");
   const app = express();
   app.listen(3000, () => {
   console.log("Server is running at http://localhost:3000");
   });

6. Install the nodemon package for automatically running the server as- npm i --save-dev nodemon (For Developing purpose)
7. setup the package.json file in the scripts key, write
   "scripts": {
   "start": "node ./resources/backend/server.js",
   "dev": "nodemon ./resources/backend/server.js",
   "test": "echo \"Error: no test specified\" && exit 1"
   },
8. use the Morgan package for automatic restart. Hence install the morgan package as npm install --save-dev morgan (Development purpose)
   Write code in the server file for initialization
   const morgan = require("morgan");
   app.use(morgan("dev")); --> Middlewire.
9. Install Postman software for API testing by the URL endpoint.
10. Install Mongobd + MongobdCompass and Mongoshell (For Database)

## ========== Connect MongoDB Database ==========

1. Install Mondodb + Mongodb Compass and Mongodb Shell download from the google.
2. Set up Environment Variable in drive:c/program file
3. Create a directory in the base path of the c drive named data. Inside the data directory create another folder db.
4. Write the command in the CMD window as Mongod. And write the other command in the other CMD window as mongosh.
5. Then Check the version as mongod --version and mongosh --version.
6. Install mongoose package as npm i mongoose
7. Create an atlas account. In the atlas account create a cluster that have a user(as atlas admin) and network access with any access IP address.
8. Connect the database using URL from the atlas cluster or local Mongodb compass using the mongoose package as mongoose. connect('mongodb://localhost:27017/database-name);

## How to use this template

- Clone project in your local machine
- Run the command in the root directory (Client)

```cmd
cd client
npm install
npm start

```

- Run the command in the root directory using another terminal (Server)

```cmd
cd server
npm install
npm start

```

- Visit project in your browser using path -> `http://localhost:8000`

## Configuration (If needed)

- Step-1: Setup .env file in the server folder

```env
SERVER_PORT=8080
MONGODB_URL=
JWT_ACCOUNT_ACTIVATION_KEY=
JWT_RESET_PASSWORD_KEY=
JWT_ACCESS_TOKEN_KEY=
JWT_REFRESH_TOKEN_KEY=
SMTP_USERNAME=YOUR_GMAIL_HERE
SMTP_PASSWORD=
CLIENT_URL=
SESSION_SECRET=
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=

```

- Step-2: Setup for secrect key

```js
require("dotenv").config();

const dev = {
  db: {
    mongoURL:
      process.env.MONGODB_URL || "mongodb://127.0.0.1:27017/database-name",
  },
  app: {
    port: process.env.SERVER_PORT || 8000,
    jwtAccountActivationKey: process.env.JWT_ACCOUNT_ACTIVATION_KEY,
    jwtResetPasswordKey: process.env.JWT_RESET_PASSWORD_KEY,
    jwtAcessTokenKey: process.env.JWT_ACCESS_TOKEN_KEY,
    jwtRefreshTokenKey: process.env.JWT_REFRESH_TOKEN_KEY,
    smtpUsername: process.env.SMTP_USERNAME,
    smtpPassword: process.env.SMTP_PASSWORD,
    clientUrl: process.env.CLIENT_URL,
    googleClientId: process.env.GOOGLE_CLIENT_ID,
    googleClientSecret: process.env.GOOGLE_CLIENT_SECRET,
  },
};

module.exports = dev;
```

## Working Principle

- /test -> health check (D)

  - setup morgan
  - create responseHandler - errorResponse, successResponse
  - handle http errors
  - test from Postman

- /seed -> seeding some data (D)

  - crate dummy data
  - store in database

- /api/users

  - POST /register -> create the user account (D)
    - get multi-part form data from the request body using multer
    - input validation check -> presence, image size, user exist
    - password hashing with bcrypt
    - create a jwt for storing user data temporarily
    - send email with nodemailer (SMPTP gmail username, password)
  - POST /activate -> activate the user account (D)
    - get the jwt from request
    - check existance of jwt
    - verify the jwt & decode the data
    - create & save the new user
  - GET /profile -> get the user account (D)
    - get the id from request body
    - findById()
    - send response based on user found or not
    - handle the mongoose Cast error
  - DELETE /:id -> delete the user account (D)
    - get the id from request body
    - findById(id)
    - if found delete the image from the server folder
    - findByIdAndDelete(id)
    - clear the cookies
    - send response
  - PUT /:id -> update the user account (D)
    - get the data from request body and params
    - create filter, updates, options
    - check image exist -> image size -> change updates
    - findByIdAndUpdate(filter, updates, options)
    - if user was updated then send response
  - PUT /update-password/:id -> update the password
    - aa
  - POST /forget-password -> forget the password
  - PUT /reset-password -> reset the password
  - PUT /ban/:id -> ban the user
  - PUT /unban/:id -> unban the user
  - GET - Admin - /all-users -> get all users including search & pagination (D)
    - get data from request body
    - search users using regex
    - include pagination
    - send response

- /api/auth (JWT Auth)

  - POST /login -> isLoggedOut -> user login (D)
    - middlewares: validateUserLogin, runValidation using express-validator, isLoggedOut
    - extract request body
    - check user's existance
    - compare the password & return response
    - check user is banned & return response
    - create jwt token with an expiry time
    - create http only cookie with less time
  - POST /logout -> isLoggedIn -> user logout (D)
    - clear the cookie
    - send the response
  - GET /refresh -> get refresh token (D)
    - get old access token from cookie
    - verify old token
    - if verified - clear exisitng cookie, create refresh token (new token), cookie, return refresh token

- Middleware

  - isLoggedIn (D)
  - isLoggedOut
  - isAdmin
  - uploadFile
  - getRefreshToken
  - userValidation

- /api/blogs

  - POST / -> search the blog (Admin/User)
  - POST /search-blogs -> search the blog (Admin/User)
  - GET /:id -> get single blog
  - POST / -> create a blog (Admin)
  - DELETE /:id -> delete a blog (Admin)
  - PUT /:id -> update a blog (Admin)

- package that we will need
  `npm install express cors http-errors multer body-parser bcrypt jsonwebtoken nodemailer cookie-parser`
  `npm install --save-dev morgan nodemon`

## Follow Me

[<img src='https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/github.svg' alt='github' height='40'>](https://github.com/learnwithfair) [<img src='https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/facebook.svg' alt='facebook' height='40'>](https://www.facebook.com/learnwithfair/) [<img src='https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/instagram.svg' alt='instagram' height='40'>](https://www.instagram.com/learnwithfair/) [<img src='https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/twitter.svg' alt='twitter' height='40'>](https://www.twiter.com/learnwithfair/) [<img src='https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/youtube.svg' alt='YouTube' height='40'>](https://www.youtube.com/@learnwithfair)

<!-- MARKDOWN LINKS & IMAGES -->

[youtube-shield]: https://img.shields.io/badge/-Youtube-black.svg?style=flat-square&logo=youtube&color=555&logoColor=white
[youtube-url]: https://youtube.com/@learnwithfair
[facebook-shield]: https://img.shields.io/badge/-Facebook-black.svg?style=flat-square&logo=facebook&color=555&logoColor=white
[facebook-url]: https://facebook.com/learnwithfair
[instagram-shield]: https://img.shields.io/badge/-Instagram-black.svg?style=flat-square&logo=instagram&color=555&logoColor=white
[instagram-url]: https://instagram.com/learnwithfair
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=flat-square&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/company/learnwithfair
