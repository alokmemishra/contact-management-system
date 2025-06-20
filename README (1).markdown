# Contact Management System

## Overview
This is a backend for a Contact Management System, built as part of the Backend Intermediate Level Assignment No. 2. It enables users to manage and store contact information, including creating, updating, and deleting contact entries with details such as names, phone numbers, emails, and associated accounts. The application is developed using the JavaScript stack with Express.js, Node.js, and MongoDB.

## Features
- Create new contact entries with names, phone numbers, emails, and account details.
- Retrieve all contacts or a specific contact by ID.
- Update contact information (e.g., phone or email).
- Delete contacts.
- Efficiently organize personal data for CRUD operations and user data management.

## Tech Stack
- **Backend Framework**: Express.js
- **Runtime**: Node.js
- **Database**: MongoDB

## Prerequisites
- Node.js (v24.2.0 or later recommended)
- MongoDB (local installation or MongoDB Atlas)
- npm (Node Package Manager)

## Project Structure
```
contact-management-system/
├── models/
│   └── Contact.js      # Mongoose schema for contacts
├── routes/
│   └── contacts.js     # API routes for contact operations
├── .env                # Environment variables
├── server.js           # Main server file
└── package.json        # Project dependencies and scripts
└── README.md           # Project documentation
```

## Setup Instructions

### 1. Clone or Download the Project
If you haven't already, place the project files in a directory:
```bash
mkdir contact-management-system
cd contact-management-system
```

### 2. Install Dependencies
Install the required npm packages:
```bash
npm install
```

This will install the following dependencies:
- `express`
- `mongoose`
- `cors`
- `dotenv`

### 3. Set Up Environment Variables
Create a `.env` file in the root directory with the following content:
```
PORT=5002
MONGO_URI=mongodb://127.0.0.1:27017/contact-management
```

- `PORT`: The port where the server will run (set to 5002 as per your setup).
- `MONGO_URI`: The MongoDB connection string. If using MongoDB Atlas, replace this with your Atlas connection string (e.g., `mongodb+srv://<username>:<password>@cluster0.mongodb.net/contact-management`).

### 4. Start MongoDB
Ensure MongoDB is running on your machine:
- If using a local MongoDB instance:
  ```bash
  brew services start mongodb-community
  ```
  Or run manually:
  ```bash
  mongod
  ```
- Verify MongoDB is running on port `27017`:
  ```bash
  lsof -i :27017
  ```
- If using MongoDB Atlas, ensure your cluster is active and the `MONGO_URI` is correctly set in the `.env` file.

### 5. Start the Server
Run the server:
```bash
node server.js
```

You should see:
```
Server running on port 5002
MongoDB connected
```

If you encounter a MongoDB connection error (`ECONNREFUSED`), ensure MongoDB is running and the `MONGO_URI` is correct.

## API Endpoints
The server runs on `http://localhost:5002`. Below are the available endpoints:

- **GET /**  
  Root route to confirm the server is running.  
  Response: `Welcome to the Contact Management System API! Use /api/contacts to manage contacts.`

- **POST /api/contacts**  
  Create a new contact.  
  Example Request Body:
  ```json
  {
    "name": "John Doe",
    "phone": "123-456-7890",
    "email": "john@example.com",
    "account": "Acme Corp"
  }
  ```
  Example: Use `curl` to test:
  ```bash
  curl -X POST http://localhost:5002/api/contacts \
  -H "Content-Type: application/json" \
  -d '{"name": "John Doe", "phone": "123-456-7890", "email": "john@example.com", "account": "Acme Corp"}'
  ```

- **GET /api/contacts**  
  Retrieve all contacts.  
  Example: `http://localhost:5002/api/contacts`  
  Response: Array of contacts (e.g., `[{"name":"John Doe",...}]`)

- **GET /api/contacts/:id**  
  Retrieve a specific contact by ID.  
  Example: `http://localhost:5002/api/contacts/<contact-id>`  
  Response: Contact object or `{ message: 'Contact not found' }` if not found.

- **PUT /api/contacts/:id**  
  Update a contact by ID.  
  Example Request Body:
  ```json
  {
    "phone": "098-765-4321",
    "email": "john.doe@newdomain.com"
  }
  ```
  Example: Use `curl` to test:
  ```bash
  curl -X PUT http://localhost:5002/api/contacts/<contact-id> \
  -H "Content-Type: application/json" \
  -d '{"phone": "098-765-4321"}'
  ```

- **DELETE /api/contacts/:id**  
  Delete a contact by ID.  
  Example: `http://localhost:5002/api/contacts/<contact-id>`  
  Response: `{ message: 'Contact deleted' }`

## Troubleshooting
- **MongoDB Connection Error**:
  - Ensure MongoDB is running on `127.0.0.1:27017`.
  - Check MongoDB logs: `cat /usr/local/var/log/mongodb/mongo.log`.
  - If local MongoDB fails, consider using MongoDB Atlas (see setup instructions above).
- **Port Conflict**:
  - Check if port `5002` is in use: `lsof -i :5002`.
  - Kill the process using the port: `kill -9 <PID>` (replace `<PID>` with the process ID), or change the `PORT` in `.env` to another value (e.g., `5003`).
- **CORS Issues**:
  - Ensure the frontend (if used) is configured to allow requests to `http://localhost:5002`.

## License
This project is for educational purposes as part of the Backend Intermediate Level Assignment No. 2.