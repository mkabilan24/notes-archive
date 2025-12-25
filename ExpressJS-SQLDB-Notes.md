## Notes for express JS

> The Express js framework is a minimal and flexible node.js web application framework that provides a robust set of feature for the application development

Following are some of the keyfeatures for the application development

1. Fast and minimialistic
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

### Path Framework

SQL DB -> dbHelper -> Repository -> Service -> Controller -> Routes (Acts Like A GateWay)

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

3. Create a directories for the application
    - service : User.service.js
    - controller: User.controller.js
    - routes: User.routes.js
    - repository: User.repository.js

4. Adding the swagger for the application development

```Bash

npm install --save swagger-jsdoc swagger-ui-express

```

5. Get the basic sql js file

```Bash

npm install --save sql.js

```
6. Install CORS - Cross Origin Resource Sharing

```Bash

npm install cors

```

7. Add dbHelper.js in repository folder and create userdb file in main folder

```JavaScript : dbHelper.js

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

```

8. Create server.js file in main project file, and add the Server Start Up, the swagger             application, CORS, dbHelper in server.js

```javascript
    const Express = require("express");
    const swaggerUi = require('swagger-ui-express');
    const swaggerJsDoc = require('swagger-jsdoc');
    const app = Express();
    const userRouter = require("./routes/user.routes");
    const { initDB } = require("./repository/dbHelper");

    const cors = require("cors");
    app.use(cors());

    initDB()
    // const port
    const PORT = 3000;

    const swaggerOptions = {
        swaggerDefinition: {
            openapi: '3.0.0',
            info: {
                title: 'My Customer API',
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

9. Update the repository layer for the application in repository folder

```JavaScript : user.repository.js

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

10. Working with the service in the service folder

```JavaScript : user.service.js

    const { UserRepository } = require("../repository/user.repository");

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

11. Updating the controller in the controller folder

```Javascript : user.controller.js
    const { UserService } = require("../service/user.service");

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

12. Updating the routes file for the application in the routes folder

```JavaScript : user.routes.js

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
const { UserController } = require("../controller/user.controller");
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
router.post('/', (req, res) => new UserController().save(req, res))

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

13. Additional Info
    To Open Swagger UI - http://localhost:3000/api-docs/
    To start the server - 
        ```Bash
            npm run start
        ```
    For help in npm commands
        ```Bash
            npm --help
        ```