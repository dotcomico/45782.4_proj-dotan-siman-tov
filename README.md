# admin  eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NCwicm9sZSI6ImFkbWluIiwiaWF0IjoxNzY3Mzg5MDE5LCJleHAiOjE3Njc5OTM4MTl9.lCCRPR8HbDWh7XS5A3BVImkIipn_ag-7S3D74HkgCUc
# maneger
# customer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6Mywicm9sZSI6ImN1c3RvbWVyIiwiaWF0IjoxNzY3Mzg4OTMyLCJleHAiOjE3Njc5OTM3MzJ9.ZwE69gUyFpE3d7PkjuJ03LMzIixyfl8nmFbcyk05e-g

supermarket-api/
├── node_modules/
├── public/
│   └── uploads/          <-- Images saved by Multer
├── src/
│   ├── config/
│   │   ├── database.js   <-- Sequelize connection
│   │   └── constants.js  <-- [NEW] Global ROLES and ORDER_STATUS
│   ├── middleware/
│   │   ├── auth.js       <-- JWT verification
│   │   ├── checkRole.js  <-- Uses ROLES constant
│   │   └── multer.js     <-- File upload logic
│   ├── models/
│   │   ├── User.js       <-- Updated with ROLES enum
│   │   ├── Product.js    <-- Name, price, stock, image
│   │   ├── Order.js      <-- Updated with ORDER_STATUS enum
│   │   └── OrderItem.js  <-- Bridge table (Snapshot of price/qty)
│   ├── controllers/      <-- [NEW] Heavy logic lives here
│   │   ├── authController.js
│   │   ├── productController.js
│   │   └── orderController.js
│   ├── routes/
│   │   ├── auth.js       
│   │   ├── users.js      <-- [NEW] Admin user management
│   │   ├── products.js   
│   │   └── orders.js     
│   └── server.js         <-- Entry point & Model Associations
├── .env                  <-- JWT_SECRET, PORT
└── package.json

## Phase 1: Backend Foundation & Configuration
Before writing business logic, set up the "plumbing" of your application.

[ ] Environment Setup: Create a .env file to store sensitive data like PORT, JWT_SECRET, and DB_NAME.✅

[ ] Sequelize Connection: In a new config/database.js (or within server.js), initialize Sequelize to connect to SQLite.✅

Key Concept: new Sequelize({ dialect: 'sqlite', storage: './database.sqlite' }).✅

[ ] Server Entry Point (server.js): * Set up Express app, use cors(), express.json(), and express.static('public/uploads') to serve images.

Use ES6 Modules: Ensure "type": "module" is in your package.json.✅

## Phase 2: Models & Database Schema (ORM)
Define how your data looks. Since it's a supermarket app, you need Users, Products, and Orders.

[ ] User Model (models/User.js):

Key Concept: sequelize.define('User', { ... }).

Fields: username, email, password, and role (enum: 'admin', 'manager', 'customer').

[ ] Product & Order Models: Create models for items and transactions.

[ ] Associations: Define relationships (e.g., User.hasMany(Order)).

## Phase 3: Security & Middleware
This is the "brain" of your RBAC (Role-Based Access Control) and Authentication.

[ ] Auth Middleware (middleware/auth.js):

Key Concept: jwt.verify(token, process.env.JWT_SECRET).

This extracts the user ID from the header and attaches it to req.user.

[ ] Role Middleware (middleware/checkRole.js):

Create a function that checks if req.user.role matches the required role for a route.

[ ] Password Hashing: Use bcrypt.hash during registration and bcrypt.compare during login.

## Phase 4: Routes & Business Logic (CRUD)
Connect your models to the internet via Express routes.

[ ] Auth Routes: POST /register and POST /login.

[ ] Product Routes (with Multer): * Key Concept: upload.single('image'). Use Multer to handle the file upload before saving the file path to the database.

[ ] Order Routes: Implement logic for "buying." Ensure the user is authenticated before allowing an order to be created.

## Phase 5: Frontend Development (React + Vite)
Now, build the interface to consume your API.

[ ] Folder Structure: Create folders for components, pages, hooks, and services.

[ ] Axios Instance: Create a services/api.js file to set the baseURL so you don't type http://localhost:5000 every time.

[ ] Authentication State: Use useContext or a state manager to keep track of the logged-in user and their JWT.

[ ] Protected Routes: Create a component that redirects users to /login if they aren't authenticated or don't have the right role.

[ ] Forms & Validation: Use useState to handle inputs for adding products (Admin) or checking out (Customer).

#### Term,Implementation Detail
RBAC,       Restricting routes based on user.role (Admin vs Customer).
JWT,        Sent in the Authorization: Bearer <token> header.
Multer,     Middleware for multipart/form-data (Image uploads).
Bcrypt,     saltRounds = 10 is the standard for hashing.
Sequelize,  Use .sync() to generate tables in your SQLite file.
CRUD,       Create (POST), Read (GET), Update (PUT), Delete (DELETE).