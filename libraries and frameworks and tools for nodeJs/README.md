# libraries and frameworks and tools for nodeJs

## Web Frameworks:
### 1. Express.js
**Description**: A minimal and flexible web application framework for Node.js, providing a robust set of features for web and mobile applications.

**Usage**:
```javascript
const express = require('express');
const app = express();
const PORT = 3000;

app.get('/', (req, res) => {
    res.send('Hello World!');
});

app.listen(PORT, () => {
    console.log(`Server is running on ${PORT}`);
});
```

### 2. Koa.js
**Description**: A lightweight and modern web framework designed by the creators of Express, utilizing async/await for better control flow.

**Usage**:
```javascript
const Koa = require('koa');
const app = new Koa();

app.use(async ctx => {
    ctx.body = 'Hello World!';
});

app.listen(3000, () => {
    console.log('Server is running on http://localhost:3000');
});
```
### 3. Hapi.js
**Description**: A rich framework for building applications and services known for its powerful plugin system and configuration-driven approach.

**Usage**:
```javascript
const Hapi = require('@hapi/hapi');
const init = async () => {
    const server = Hapi.server({ port: 3000 });

    server.route({
        method: 'GET',
        path: '/',
        handler: (request, h) => {
            return 'Hello World!';
        }
    });

    await server.start();
    console.log('Server running on %s', server.info.uri);
};
init();
```

### 4. NestJS
**Description**: A progressive Node.js framework for building efficient, reliable, and scalable server-side applications, heavily inspired by Angular.

**Usage**:
```javascript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
    const app = await NestFactory.create(AppModule);
    await app.listen(3000);
}
bootstrap();
```

### 5. Sails.js
**Description**: A framework for building Node.js applications that resemble the MVC pattern, particularly suited for data-driven APIs.

**Usage**: (Typically requires scaffolding with the Sails CLI)
```bash
sails new myApp
cd myApp
sails lift
```

### 6. Fastify
**Description**: A fast and low-overhead web framework for Node.js, focusing on performance and developer experience.

**Usage**:
```javascript
const fastify = require('fastify')({ logger: true });

fastify.get('/', async (request, reply) => {
    return { hello: 'world' };
});

fastify.listen(3000, (err) => {
    if (err) {
        fastify.log.error(err);
        process.exit(1);
    }
    fastify.log.info(`Server listening on ${fastify.server.address().port}`);
});
```

## Database Libraries

### 1. Mongoose
**Description**: An ODM (Object Data Modeling) library for MongoDB and Node.js, providing a schema-based solution to model application data.

**Usage**:
```javascript
const mongoose = require('mongoose');
mongoose.connect('mongodb://localhost/test');

const Cat = mongoose.model('Cat', { name: String });
const kitty = new Cat({ name: 'Zildjian' });
kitty.save().then(() => console.log('meow'));
```

### 2. Sequelize
**Description**: A promise-based Node.js ORM for various SQL databases, including PostgreSQL, MySQL, SQLite, and MSSQL.

**Usage**:
```javascript
const { Sequelize, DataTypes } = require('sequelize');
const sequelize = new Sequelize('sqlite::memory:');

const User = sequelize.define('User', {
    username: {
        type: DataTypes.STRING,
        unique: true
    }
});

(async () => {
    await sequelize.sync();
    const user = await User.create({ username: 'janedoe' });
    console.log(user.toJSON());
})();
```

### 3. Knex.js
**Description**: A SQL query builder for Node.js, allowing for flexible and powerful database interaction.

**Usage**:
```javascript
const knex = require('knex')({
    client: 'sqlite3',
    connection: {
        filename: "./mydb.sqlite"
    }
});

knex('users').insert({ name: 'John Doe' }).then(() => console.log('User added'));
```

### 4. TypeORM
**Description**: An ORM for TypeScript and JavaScript (ES7, ES6, ES5), supporting various SQL and NoSQL databases.

**Usage**:
```javascript
import "reflect-metadata";
import { createConnection } from "typeorm";

createConnection().then(async connection => {
    // Your code here
});
```

## Authentication Libraries:

### 1. Passport.js
**Description**: A middleware for Node.js that simplifies authentication, supporting various strategies, including OAuth and local authentication.

**Usage**:
```javascript
const passport = require('passport');
const LocalStrategy = require('passport-local').Strategy;

passport.use(new LocalStrategy((username, password, done) => {
    // Verify username and password
}));
```

### 2. JSON Web Token (jsonwebtoken)
**Description**: A library for working with JSON Web Tokens (JWT) for authentication and information exchange.

**Usage**:
```javascript
const jwt = require('jsonwebtoken');
const token = jwt.sign({ userId: 123 }, 'your-256-bit-secret');
```

### 3. bcrypt.js
**Description**: A library for hashing passwords, providing a strong hashing algorithm for security.

**Usage**:
```javascript
const bcrypt = require('bcrypt');
const saltRounds = 10;

bcrypt.hash('myPlaintextPassword', saltRounds, (err, hash) => {
    // Store hash in your password DB
});
```

## Testing Libraries:

### 1. Mocha
**Description**: A feature-rich JavaScript test framework running on Node.js, allowing for asynchronous testing.

**Usage**:
```javascript
const assert = require('assert');

describe('Array', function() {
    describe('#indexOf()', function() {
        it('should return -1 when the value is not present', function() {
            assert.equal([-1, 0, 1].indexOf(2), -1);
        });
    });
});
```

### 2. Chai
**Description**: An assertion library that works with Mocha, providing various interfaces for assertions (should, expect, assert).

**Usage**:
```javascript
const chai = require('chai');
const expect = chai.expect;

describe('Array', function() {
    it('should be an array', function() {
        expect([1, 2, 3]).to.be.an('array');
    });
});
```

### 3. Jest
**Description**: A delightful JavaScript testing framework maintained by Facebook, providing a zero-config setup and support for snapshots.

**Usage**:
```javascript
test('adds 1 + 2 to equal 3', () => {
    expect(1 + 2).toBe(3);
});
```
### 4. Supertest
**Description**: A library for testing HTTP servers in Node.js, often used in conjunction with Mocha or Jest.

**Usage**:
```javascript
const request = require('supertest');
const app = require('./app'); // Your Express app

describe('GET /', function() {
    it('responds with json', function(done) {
        request(app)
            .get('/')
            .expect('Content-Type', /json/)
            .expect(200, done);
    });
});
```

### 5. Sinon
**Description**: A standalone library for creating spies, mocks, and stubs in JavaScript, making it easy to test asynchronous code and APIs.

**Usage**:
```javascript
const sinon = require('sinon');

const myObj = {
    myMethod: function() {}
};

const spy = sinon.spy(myObj, 'myMethod');
myObj.myMethod();
console.log(spy.called); // true
```

### 6. Nock

**Description**: Nock is an HTTP mocking and expectations library for Node.js, allowing you to test HTTP requests without making real network calls.

**Usage**:
```javascript
const nock = require('nock');

nock('http://example.com')
    .get('/users')
    .reply(200, { id: 1, name: 'John Doe' });

// Your test code to make a request to http://example.com/users
```

### 7. Jasmine
**Description**: Jasmine is a behavior-driven development framework for testing JavaScript code. It provides a clean syntax for writing tests and is often used in conjunction with other libraries like Sinon for mocking.

**Usage**:

```javascript
describe("A suite is just a function", function() {
    it("and so is a spec", function() {
        expect(true).toBe(true);
    });
});
```

### 8. AVA
**Description**: AVA is a test runner for Node.js that runs tests concurrently, which can lead to faster test execution. It has a minimalistic API and is designed for simplicity.

**Usage**:

```javascript
import test from 'ava';

test('foo', t => {
    t.pass();
});
```
### 9. Puppeteer
**Description**: Puppeteer is a Node library that provides a high-level API to control Chrome or Chromium over the DevTools protocol. It is commonly used for testing web applications and automating browser tasks.

**Usage**:

```javascript
const puppeteer = require('puppeteer');

(async () => {
    const browser = await puppeteer.launch();
    const page = await browser.newPage();
    await page.goto('https://example.com');
    await page.screenshot({ path: 'example.png' });
    await browser.close();
})();
```

## Real-Time Communication

### 1. Socket.io
**Description**: Socket.io is a library for real-time web applications, enabling bi-directional communication between clients and servers. It abstracts the complexities of WebSocket and provides a simple API for developers.

**Usage**:
```javascript
const express = require('express');
const http = require('http');
const socketIo = require('socket.io');

const app = express();
const server = http.createServer(app);
const io = socketIo(server);

io.on('connection', (socket) => {
    console.log('a user connected');
    socket.on('disconnect', () => {
        console.log('user disconnected');
    });
});

server.listen(3000, () => {
    console.log('listening on *:3000');
});
```

### 2. ws
**Description**: `ws` is a simple and efficient WebSocket implementation for Node.js. It provides a straightforward API for creating WebSocket servers and clients.

**Usage**:
```javascript
const WebSocket = require('ws');

const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', (ws) => {
    ws.on('message', (message) => {
        console.log(`Received: ${message}`);
    });
    ws.send('Hello! Message from server.');
});
```

## Node.js Utility Libraries

### 1. Lodash
**Description**: Lodash is a modern JavaScript utility library delivering modularity, performance, and extras. It provides helpful functions for manipulating arrays, objects, and other data types.

**Usage**:
```javascript
const _ = require('lodash');

const array = [1, 2, 3, 4];
const reversed = _.reverse(array.slice());
console.log(reversed); // [4, 3, 2, 1]
```
### 2. Moment.js
**Description**: Moment.js is a library for parsing, validating, manipulating, and displaying dates and times in JavaScript. It simplifies date handling and formatting.

**Usage**:
```javascript
const moment = require('moment');

const now = moment();
console.log(now.format('MMMM Do YYYY, h:mm:ss a')); // e.g., "August 22nd 2024, 10:03:00 am"
```

### 3. Axios
**Description**: Axios is a promise-based HTTP client for the browser and Node.js, allowing easy communication with APIs. It supports request and response interception, automatic JSON data transformation, and more.

**Usage**:
```javascript
const axios = require('axios');

axios.get('https://api.example.com/data')
    .then(response => {
        console.log(response.data);
    })
    .catch(error => {
        console.error(error);
    });
```

### 4. Node-fetch
**Description**: Node-fetch is a lightweight module that brings `window.fetch` to Node.js, allowing for making HTTP requests using the Fetch API.

**Usage**:
```javascript
const fetch = require('node-fetch');

fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error(error));
```

## File Upload and Processing

### 1. Multer
**Description**: Multer is a middleware for handling `multipart/form-data`, primarily used for uploading files in Node.js applications.

**Usage**:
```javascript
const express = require('express');
const multer = require('multer');
const upload = multer({ dest: 'uploads/' });

const app = express();

app.post('/upload', upload.single('file'), (req, res) => {
    res.send('File uploaded successfully.');
});

app.listen(3000, () => {
    console.log('Server is running on port 3000');
});
```

### 2. Sharp
**Description**: Sharp is a high-performance image processing library for Node.js, allowing for resizing, cropping, and manipulating images efficiently.

**Usage**:
```javascript
const sharp = require('sharp');

sharp('input.jpg')
    .resize(200, 200)
    .toFile('output.jpg', (err, info) => {
        if (err) throw err;
        console.log(info);
    });
```

## Task Runners and Build Tools:

### 1. Gulp
**Description**: Gulp is a toolkit for automating time-consuming tasks in your development workflow. It uses a code-over-configuration approach to define tasks.

**Usage**:
```javascript
const gulp = require('gulp');

gulp.task('default', () => {
    return gulp.src('src/*.js')
        .pipe(gulp.dest('dist'));
});
```

### 2. Grunt
**Description**: Grunt is a JavaScript task runner that automates repetitive tasks, such as minification, compilation, and testing.

**Usage**:
```javascript
module.exports = function(grunt) {
    grunt.initConfig({
        pkg: grunt.file.readJSON('package.json'),
        uglify: {
            build: {
                src: 'src/app.js',
                dest: 'dist/app.min.js'
            }
        }
    });

    grunt.loadNpmTasks('grunt-contrib-uglify');
    grunt.registerTask('default', ['uglify']);
};
```

### 3. Webpack
**Description**: Webpack is a module bundler for modern JavaScript applications, allowing for efficient asset management and code splitting.

**Usage**:
```javascript
const path = require('path');

module.exports = {
    entry: './src/index.js',
    output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist')
    }
};
```

## API Development:

## 1. Apidoc
**Description**: Apidoc is a tool to generate API documentation directly from your code comments, making it easy to maintain up-to-date documentation.

**Usage**:
```javascript
/**
 * @api {get} /users Request Users information
 * @apiName GetUsers
 * @apiGroup User
 *
 * @apiSuccess {String} id User's unique ID.
 * @apiSuccess {String} name User's name.
 */
```

### 2. Swagger
**Description**: Swagger is a framework for API development that includes tools for API documentation, testing, and client generation. It helps in designing and documenting RESTful APIs.

**Usage**:
```javascript
const swaggerJsDoc = require('swagger-jsdoc');
const swaggerUi = require('swagger-ui-express');

const swaggerOptions = {
    swaggerDefinition: {
        openapi: '3.0.0',
        info: {
            title: 'My API',
            version: '1.0.0',
        },
    },
    apis: ['./routes/*.js'],
};

const swaggerDocs = swaggerJsDoc(swaggerOptions);
app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerDocs));
```

## Other Notable Libraries:

### 1. Bull
**Description**: Bull is a robust queue package for handling distributed jobs and messages in Node.js. It is built on Redis and provides a simple API for job management.

**Usage**:
```javascript
const Queue = require('bull');

const myQueue = new Queue('my-queue');

myQueue.process((job, done) => {
    console.log(job.data);
    done();
});

myQueue.add({ foo: 'bar' });
```

### 2. Nodemailer
**Description**: Nodemailer is a module for sending emails from Node.js applications. It supports various transport methods, including SMTP and direct transport.

**Usage**:
```javascript
const nodemailer = require('nodemailer');

const transporter = nodemailer.createTransport({
    service: 'gmail',
    auth: {
        user: 'your-email@gmail.com',
        pass: 'your-password'
    }
});

const mailOptions = {
    from: 'your-email@gmail.com',
    to: 'recipient@example.com',
    subject: 'Hello',
    text: 'Hello world!'
};

transporter.sendMail(mailOptions, (error, info) => {
    if (error) {
        return console.log(error);
    }
    console.log('Email sent: ' + info.response);
});
```

### 3. SocketCluster
**Description**: SocketCluster is a real-time framework that allows you to build scalable applications with WebSocket support. It provides a simple API for creating real-time applications.

**Usage**:
```javascript
const socketCluster = require('socketcluster-server');

const app = socketCluster.listen(8000);

app.on('connection', (socket) => {
    console.log('Client connected');
    socket.on('disconnect', () => {
        console.log('Client disconnected');
    });
});
```

### 4. Express Validator

**Description**: Express Validator is a set of middlewares for validating and sanitizing user input in Express applications. It helps ensure that incoming data meets specified criteria.

**Usage**:
```javascript
const { body, validationResult } = require('express-validator');

app.post('/user', [
    body('email').isEmail(),
    body('password').isLength({ min: 5 })
], (req, res) => {
    const errors = validationResult(req);
    if (!errors.isEmpty()) {
        return res.status(400).json({ errors: errors.array() });
    }
    res.send('User is valid');
});
```

## Delivery of images and videos:

### Cloudinary Library
**Description**: The Cloudinary Node.js library is an open-source SDK that allows developers to easily integrate their applications with Cloudinary's powerful media API. This library enables efficient management, transformation, optimization, and delivery of images and videos through multiple CDNs.

**Features**:
- **Image and Video Uploads**: Easily upload images and videos to Cloudinary.
- **Transformations**: Apply various transformations to images and videos, such as resizing, cropping, and format conversion.
- **Optimizations**: Automatically optimize media for faster delivery.
- **CDN Delivery**: Deliver media through Cloudinary's global CDN for improved performance.

#### Installation

- To install the Cloudinary Node.js library, use npm:

```bash
npm install cloudinary
```

**Configuration**:
To use the Cloudinary library, you need to configure it with your Cloudinary credentials. At a minimum, you will need your cloud_name, api_key, and api_secret.

```javascript
const cloudinary = require('cloudinary').v2;

cloudinary.config({
  cloud_name: 'your-cloud-name',
  api_key: 'your-api-key',
  api_secret: 'your-api-secret'
});
```

**Usage**:
- Uploading an Image
Here’s a simple example of how to upload an image to Cloudinary:

```javascript
cloudinary.uploader.upload('path/to/image.jpg', (error, result) => {
  if (error) {
    console.error('Upload failed:', error);
  } else {
    console.log('Upload successful:', result);
  }
});
```

- Transforming an Image
You can also apply transformations when delivering images:

```javascript
const imageUrl = cloudinary.url('sample', {
  width: 300,
  height: 300,
  crop: 'fill'
});

console.log('Transformed Image URL:', imageUrl);
```
## maintaining code quality:

### ESLint
A tool for maintaining code quality and consistency in JavaScript applications, including Node.js. It analyzes code to identify and fix issues based on defined rules.

**Description**

ESLint helps developers adhere to best practices and maintain a consistent code style. It allows for custom rules or predefined configurations, aiding in error detection, coding standards enforcement, and improved readability.

#### Installation Steps:

- Initialize your Node.js project:


```bash
npm init -y
```

- Install ESLint:

```bash
npm install eslint --save-dev
```

- Initialize ESLint configuration:

```bash
npx eslint --init
```

During setup, you'll answer questions about your project, including usage, module type, TypeScript usage, style guide preference, and environment.

**Usage**:

- Run ESLint on specific files or directories:

```bash
npx eslint src/**/*.js
```

- Fix Issues Automatically:


```bash
npx eslint src/**/*.js --fix
```

- onfiguration File Example:

```json
{
  "env": {
    "node": true,
    "es6": true
  },
  "extends": "eslint:recommended",
  "rules": {
    "semi": ["error", "always"],
    "quotes": ["error", "single"]
  }
}
```

***Example***

- Sample Script (index.js):

```javascript
const greet = (name) => {
    console.log('Hello, ' + name);
}

greet('World')
```
Running ESLint on this script may highlight issues like missing semicolons or inconsistent quotes.
