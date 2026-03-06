# CRUD API with Express and MongoDB

A RESTful API for managing user data built with Express.js and MongoDB using Mongoose.

## Overview

This is a professional-grade CRUD (Create, Read, Update, Delete) API that allows users to perform all basic database operations on user records. The API is built using Node.js, Express, and MongoDB.

## Prerequisites

- Node.js (v14 or higher)
- npm or yarn package manager
- MongoDB Atlas account (or local MongoDB instance)

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd homework
```

2. Install dependencies:
```bash
npm install
```

3. Configure your MongoDB connection in `index.js` if needed.

4. Start the server:
```bash
node index.js
```

The server will run on port 3000.

## API Endpoints

### Welcome Endpoint
- **GET** `/`
  - Returns API information and version

### User Operations

#### Get All Users
- **GET** `/allusers`
  - Retrieves all users from the database

#### Get User by ID
- **GET** `/user/:id`
  - Retrieves a specific user by their ID
  - Parameters: `id` (MongoDB ObjectId)

#### Add Single User
- **POST** `/adduser`
  - Creates a new user
  - Request body:
    ```json
    {
      "name": "John Doe",
      "email": "john@example.com",
      "password": "password123"
    }
    ```

#### Add Multiple Users
- **POST** `/addusers`
  - Creates multiple users at once
  - Request body: Array of user objects
    ```json
    [
      {
        "name": "User 1",
        "email": "user1@example.com",
        "password": "password123"
      },
      {
        "name": "User 2",
        "email": "user2@example.com",
        "password": "password456"
      }
    ]
    ```

#### Update User (Complete)
- **PUT** `/updateuser/:id`
  - Updates a user completely with validation
  - Parameters: `id` (MongoDB ObjectId)

#### Update User (Partial)
- **PATCH** `/updateuser/:id`
  - Updates specific fields of a user
  - Parameters: `id` (MongoDB ObjectId)

#### Delete User
- **DELETE** `/deleteuser/:id`
  - Deletes a user from the database
  - Parameters: `id` (MongoDB ObjectId)

## User Schema

The User model includes the following fields:

- `name` (String, required) - User's full name
- `email` (String, required, unique, lowercase) - User's email address
- `password` (String, required, min 6 characters) - User's password

## Usage Examples

### Using cURL

Get all users:
```bash
curl http://localhost:3000/allusers
```

Add a new user:
```bash
curl -X POST http://localhost:3000/adduser \
  -H "Content-Type: application/json" \
  -d '{"name":"Jane Doe","email":"jane@example.com","password":"secure123"}'
```

Get user by ID:
```bash
curl http://localhost:3000/user/USER_ID_HERE
```

Update a user:
```bash
curl -X PUT http://localhost:3000/updateuser/USER_ID_HERE \
  -H "Content-Type: application/json" \
  -d '{"name":"Updated Name"}'
```

Delete a user:
```bash
curl -X DELETE http://localhost:3000/deleteuser/USER_ID_HERE
```

### Using Postman

1. Import the API endpoints into Postman
2. Set the base URL to `http://localhost:3000`
3. Use the endpoint paths listed above
4. For POST/PUT/PATCH requests, set Content-Type to `application/json`

## Error Handling

The API returns appropriate HTTP status codes:

- `200` - Success
- `201` - Created
- `400` - Bad Request / Invalid input
- `404` - Not Found
- `500` - Server Error

## Dependencies

- `express` - Web framework
- `mongoose` - MongoDB ODM
- `express.json()` - Built-in JSON parser middleware

## Notes

- Email addresses are automatically converted to lowercase and must be unique
- Passwords must be at least 6 characters long
- All timestamps are handled by MongoDB
