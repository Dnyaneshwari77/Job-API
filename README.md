#### Setup

```bash
npm install && nodemon app.js
```

#### Database Connection

1. Import connect.js
2. Invoke in start()
3. Setup .env in the root
4. Add MONGO_URI with correct value

#### Routers

- auth.js
- jobs.js

#### User Model

Email Validation Regex

```regex
/^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
```

#### Register User

- Validate - name, email, password - with Mongoose
- Hash Password (with bcryptjs)
- Save User
- Generate Token
- Send Response with Token

#### Login User

- Validate - email, password - in controller
- If email or password is missing, throw BadRequestError
- Find User
- Compare Passwords
- If no user or password does not match, throw UnauthenticatedError
- If correct, generate Token
- Send Response with Token

#### Mongoose Errors

- Validation Errors
- Duplicate (Email)
- Cast Error


# Job Management API

A job management backend built with **Node.js**, **Express.js**, and **MongoDB**. This RESTful API allows users to register, login, and perform full CRUD operations on job entries they create. JWT is used for secure user authentication.

---

## 🚀 Tech Stack

- Node.js
- Express.js
- MongoDB (Mongoose)
- JWT (JSON Web Token)
- bcrypt.js
- dotenv

---

## 📁 Project Setup

### Prerequisites

- Node.js installed
- MongoDB instance (local or MongoDB Atlas)

### Installation

```bash
git clone https://github.com/Dnyaneshwari77/Job-API.git
npm install
```

### Environment Variables

Create a `.env` file in the root directory and add:

```env
PORT=5000
MONGO_URI=your_mongo_connection_string
JWT_SECRET=your_jwt_secret
JWT_LIFETIME=1d
```

---

## 🔐 User Schema

```js
{
  name: String,
  email: String,
  password: String (Hashed),
}
```

## 📄 Job Schema

```js
{
  company: String,
  position: String,
  status: "interview" | "declined" | "pending", // default: pending
  createdBy: ObjectId (ref to User),
}
```

---

## 📌 API Endpoints

### 👤 Auth Routes

#### `POST /api/v1/aut/register`

- Register a user
- Request Body:
```json
{
  "name": "John",
  "email": "john@example.com",
  "password": "123456"
}
```

#### `POST /api/v1/aut/login`

- Login and receive a JWT
- Request Body:
```json
{
  "email": "john@example.com",
  "password": "123456"
}
```

- Response:
```json
{
  "user": {
    "_id": "...",
    "name": "John"
  },
  "token": "..."
}
```

---

### 💼 Job Routes *(Require Authorization)*

All job routes require an `Authorization` header:
```
Bearer <your_token>
```

#### `GET /api/v1/job`

- Get all jobs
- Optional Query Params:
  - `status` (interview, pending, declined)
  - `createdBy` (user ID)

#### `GET /api/v1/job/:id`

- Get a job by ID

#### `POST /api/v1/job`

- Create a new job
- Request Body:
```json
{
  "company": "TCS",
  "position": "Backend Developer"
}
```

#### `PATCH /api/v1/job/:id`

- Update a job (company/position/status)

#### `DELETE /api/v1/job/:id`

- Delete a job

---

## ▶️ Run the Server

```bash
nodemon app.js
```

---

## 👩‍💻 Author

**Dnyaneshwari Pandhare**

GitHub: [@Dnyaneshwari77](https://github.com/Dnyaneshwari77)

---

## 📄 License

MIT License
