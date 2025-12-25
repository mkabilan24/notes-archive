ExpressJS Basics
## Notes for express JS

> The Express js framework is a minimal and flexible node.js web application framework that provides a robust set of feature for the application development

Following are some of the keyfeatures for the application development

1. Fast and minimilist
2. Routing
3. Middleware
4. Http Headers

### Some key concept you will be working with when working with nodejs

- Routes
    - We can handle HTTP method and routes for the specific application
    - Method like: GET, POST, PUT, PATCH, DELETE AND SO ON
- Middleware
    - The function that execute during the request-response cycle.
    - We can use in built or custom middleware
- routing params
    - we can set up path variable for dynamic url for better and cleaner code
- query parameter
    - We can also handle query parameter for the application

### How to set up the application

1. Init a package.json file

```BASH

npm init -y

```

2. install express js in the project

```Bash

npm install --save express
npm install --save-dev nodemon # this is an optional developer dependancy for the application

```

3. starting up the server

```JavaScript

const Express = require("express");
const app = Express();

// const port
const PORT = 3000;

// add the middleware for the application to take in the json data
app.use(Express.json());

// start the applicaton for running on specific port
app.listen(PORT, () => {
    console.log(`started server on port ${PORT}`); 
});

```
4. Testing a sample end point for the application

```JavaScript

app.get("/testing", (req, res) => {
    console.log(
        "testing is called"
    )
    return res.status(200).json({message : "test"})
})

```

5. Create a directories for the application
    - service : User.service.js
    - controller: User.controller.js
    - routes: User.routes.js
    - repository: User.repository.js

6. Adding the routes for the application

```Javascript

const express = require("express");
const routes = express.Router();

routes.get("/", (req, res) => console.log(`Get method for the application`);)
routes.get("/:id", (req, res) => console.log(`Get method for the application ${req.params.id}`);)
routes.post("/", (req, res) => console.log(`POST method for the application`);)

// TODO: do the same for update and delete

module.exports = routes;

```

Adding the routes to the server.js

```Javascript
const userRouter = require("./routes/User.routes");
// add the application with routes
app.use("/api/user", userRouter)
```

7. Adding the swagger for the application development

```Bash

npm install --save swagger-jsdoc swagger-ui-express

```

8. Adding the swagger application for the UI

```JavaScript

const Express = require("express");
const swaggerUi = require('swagger-ui-express');
const swaggerJsDoc = require('swagger-jsdoc');
const app = Express();
const userRouter = require("./routes/User.routes");

// const port
const PORT = 3000;

const swaggerOptions = {
    swaggerDefinition: {
        openapi: '3.0.0',
        info: {
            title: 'My API',
            version: '1.0.0',
            description: 'API documentation',
        },
        servers: [{ url: 'http://localhost:3000' }],
    },
    apis: ['./routes/*.js'], // Path to the API docs
};

const swaggerDocs = swaggerJsDoc(swaggerOptions);
app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerDocs));

// add the middleware for the application to take in the json data
app.use(Express.json());

// add the application with routes
app.use("/api/user", userRouter)

// start the applicaton for running on specific port
app.listen(PORT, () => {
    console.log(`started server on port ${PORT}`); 
});

```

```Javascript: User.routes.js

/**
 * @swagger
 * components:
 *  schemas:
 *      User:
 *          type: object
 *          required: 
 *              - id
 *              - name
 *              - role
 *          properties:
 *              id: 
 *                  type: number
 *                  description: Id for the user
 *              name: 
 *                  type: string
 *                  description: Name for the user
 *              role: 
 *                  type: string
 *                  description: Role for the user
 * 
 */

const Express = require("express");
const router = Express.Router();

/**
* @swagger
* /api/user/:
*   get:
*     summary: Returns an array of user
*     responses:
*       200:
*         description: Returns an array of user
*/
router.get('/', (req, res) => res.status(200).json({message: []});

/**
* @swagger
* /api/user/{id}:
* get:
*     summary: Get the book by id
*     parameters:
*       - in: path
*         name: id
*         schema:
*           type: string
*         required: true
*         description: The book id
*     responses:
*       200:
*         description: get a specific user
*/
router.get('/:id', (req, res) => res.status(200).json({message: "OK"});

/**
* @swagger
* /api/user/:
*   post:
*     summary: inserts users for the application
*     requestBody:
*        required: true
*        content: 
*           application/json:
*               schema:
*                   $ref: "#/components/schemas/User"
*     responses:
*       200:
*         description: Adds User to the book
*         content:
*           application/json:
*             schema:
*               $ref: "#/components/schemas/User"
*       500:
*         description: Some error while inserting the records
*         content:
*           application/json:
*             schema:
*               type: Object
 */
router.post('/', (req, res) => {
    return res.status(201).json(req.body);
})

/**
* @swagger
* /api/user/:
*   put:
*     summary: update users for the application
*     requestBody:
*        required: true
*        content: 
*           application/json:
*               schema:
*                   $ref: "#/components/schemas/User"
*     responses:
*       200:
*         description: Updates User to the book
*         content:
*           application/json:
*             schema:
*               $ref: "#/components/schemas/User"
*       500:
*         description: Some error while inserting the records
*         content:
*           application/json:
*             schema:
*               type: Object
 */
router.put('/', (req, res) => {
    return res.status(200).json(req.body);
})

/**
* @swagger
* /api/user/{id}:
*   delete:
*     summary: delete a specific user
*     parameters:
*        - in: path
*          name: id
*          schema: 
*               type: string
*          required: true
*          description: the user id
*     responses:
*       200:
*         description: delete a specific user
*/
router.delete('/:id', (req, res) => {
    return res.status(200).json({message : "deleted"});
})



module.exports = router;

```

8. Working with the repository

```JavaScript : User.repository.js

class UserRepository {

    static users = [
        {id: 1, name: "sahil", role: "admin"},
        {id: 2, name: "sid", role: "user"},
        {id: 3, name: "dave", role: "admin"},
    ];

    get() {
        return UserRepository.users;
    }

    save(user){
        UserRepository.users.push(user);
    }

    update(user) {
        UserRepository.users = UserRepository.users.map(data => {
            if(data.id == user.id){
                data = user;
            }
            return data;
        })
    }

    deleteUser(id){
        console.log(id);
        UserRepository.users = UserRepository.users.filter(data => data.id != id)
    }

    getUser(id) {
        return UserRepository.users.find(data => data.id == id);
    }


}

module.exports = {UserRepository};

```

9. Working with the service

```JavaScript : User.service.js

// const {UserRepository} = require("../repository/User.repository");
const { UserRepository } = require("../repository/User.repository-sql");

class UserService {

    get() {
        return new UserRepository().get();
    }

    save(user) {
        new UserRepository().save(user);
    }

    update(user) {
        new UserRepository().update(user);
    }

    deleteUser(id) {
        new UserRepository().deleteUser(id);
    }

    getUser(id) {
        return new UserRepository().getUser(id);
    }

}

module.exports = { UserService };

```

10. Working with the controller

```JavaScript

const { UserService } = require("../service/User.service");

class UserController {

    get(req, res) {
        return res.status(200).json(new UserService().get());
    }

    getUser(req, res) {
        return res.status(200).json(new UserService().getUser(req.params.id));
    }

    save(req, res) {
        return res.status(201).json(new UserService().save(req.body));
    }

    update(req, res) {
        return res.status(200).json(new UserService().update(req.body));
    }

    deleteUser(req, res) {
        return res.status(200).json(new UserService().delete(req.params.id));
    }

}

module.exports = { UserController };

```

11. Updating the routes file for the application

```JavaScript

/**
 * @swagger
 * components:
 *  schemas:
 *      User:
 *          type: object
 *          required: 
 *              - id
 *              - name
 *              - role
 *          properties:
 *              id: 
 *                  type: number
 *                  description: Id for the user
 *              name: 
 *                  type: string
 *                  description: Name for the user
 *              role: 
 *                  type: string
 *                  description: Role for the user
 * 
 */

const Express = require("express");
const {UserController} = require("../controller/User.controller");

const router = Express.Router();

/**
* @swagger
* /api/user/:
*   get:
*     summary: Returns an array of user
*     responses:
*       200:
*         description: Returns an array of user
*/
router.get('/', (req, res) => new UserController().get(req, res));

/**
* @swagger
* /api/user/{id}:
* get:
*     summary: Get the book by id
*     parameters:
*       - in: path
*         name: id
*         schema:
*           type: string
*         required: true
*         description: The book id
*     responses:
*       200:
*         description: get a specific user
*/
router.get('/:id', (req, res) => new UserController().getUser(req, res));

/**
* @swagger
* /api/user/:
*   post:
*     summary: inserts users for the application
*     requestBody:
*        required: true
*        content: 
*           application/json:
*               schema:
*                   $ref: "#/components/schemas/User"
*     responses:
*       200:
*         description: Adds User to the book
*         content:
*           application/json:
*             schema:
*               $ref: "#/components/schemas/User"
*       500:
*         description: Some error while inserting the records
*         content:
*           application/json:
*             schema:
*               type: Object
 */
router.post('/', (req, res) => new UserController().save(req, res));

/**
* @swagger
* /api/user/:
*   put:
*     summary: update users for the application
*     parameters:
*        - in: path
*          name: id
*          schema: 
*               type: string
*          required: true
*          description: the user id
*     requestBody:
*        required: true
*        content: 
*           application/json:
*               schema:
*                   $ref: "#/components/schemas/User"
*     responses:
*       200:
*         description: Updates User to the book
*         content:
*           application/json:
*             schema:
*               $ref: "#/components/schemas/User"
*       500:
*         description: Some error while inserting the records
*         content:
*           application/json:
*             schema:
*               type: Object
 */
router.put('/', (req, res) => new UserController().update(req, res))

/**
* @swagger
* /api/user/{id}:
*   delete:
*     summary: delete a specific user
*     parameters:
*        - in: path
*          name: id
*          schema: 
*               type: string
*          required: true
*          description: the user id
*     responses:
*       200:
*         description: delete a specific user
*/
router.delete('/:id', (req, res) => new UserController().deleteUser(req, res))



module.exports = router;

```

---

Additional steps: if you want to work with the sql part for the application update the code with following information

1. Get the basic sql js file

```Bash

npm install --save sql.js

```
2. Update the repository layer for the application

```JavaScript : User.repository.js

const { getDB, saveDB } = require("./dbHelper");

class UserRepository {

    constructor() { }

    save(user) {
        const db = getDB();
        db.run(`insert into users (id, name, role) values (?,?,?)`, [user.id, user.name, user.role]);
        saveDB();
    }

    update(user) {
        const db = getDB();
        db.run("update users set name=?, role=? where id=?", [user.name, user.role, user.id]);
        saveDB();
    }

    deleteUser(id) {
        console.log(id);
        const db = getDB();
        db.run("delete from users where id=?", [id]);
        let temp = this.get();
        console.log("=======================");
        console.log(temp);
        console.log("=======================");        
        saveDB();
    }

    get() {
        const db = getDB();
        const result = db.exec("select * from users");
        console.log(result[0]);
        const rows = result[0]?.values || [];
        const users = rows.map(([id, name, role]) => ({ id, name, role }));
        return users;
    }

    getUser(id) {
        const db = getDB();
        const result = db.exec("select * from users where id=" + id);
        console.log(result[0]);
        const rows = result[0]?.values || [];
        const users = rows.map(([id, name, role]) => ({ id, name, role }));
        return users[0] ? users[0] : [];
    }

}

module.exports = { UserRepository }

```

3. Database part for the application

```JavaScript

const fs = require("fs");
const initSqlJs = require("sql.js");
const { buffer } = require("stream/consumers");

let db;
let sql;

const initDB = async() => {
    sql = await initSqlJs();
    const fileBuffer = fs.readFileSync("userdb")
    db = new sql.Database(fileBuffer);
    db.exec(`create table if not exists users(id number, name string, role string)`)
}

const getDB = () => db;

const saveDB = () => {
    const data = db.export();
    fs.writeFileSync('userdb', Buffer.from(data));
}

module.exports = {initDB, getDB, saveDB};