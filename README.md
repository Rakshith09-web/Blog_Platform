# Blog Platform API

A RESTful API for a blog platform built with Express.js and PostgreSQL, featuring user authentication, blog post management, and commenting system.

## Prerequisites

Before you begin, ensure you have the following installed:
- Node.js (v12.0.0 or higher)
- PostgreSQL (v10 or higher)
- npm (usually comes with Node.js)

## Installation

1. Clone the repository:
```bash
git clone <your-repo-url>
cd <repo-name>
```

2. Install dependencies:
```bash
npm install
```

3. Create a `.env` file in the root directory with the following configuration:
```env
DB_USER=postgres
DB_PASSWORD=your_password
DB_HOST=localhost
DB_PORT=5432
DB_NAME=blog_db
JWT_SECRET=your_jwt_secret
PORT=3000
```

4. Set up the database:
- Open PostgreSQL command prompt or pgAdmin
- Create and set up the database using the provided SQL script:
```bash
psql -U postgres -f database.sql
```

## Running the Application

Start the server:
```bash
npm start
```

The API will be available at `http://localhost:3000`

## Running Tests

1. Set up the test database:
```bash
psql -U postgres -f test/setup/test-database.sql
```

2. Run the tests:
```bash
npm test
```

## API Endpoints

### Authentication
- **Register User**
  - POST `/api/auth/register`
  - Body: `{ "username": "string", "email": "string", "password": "string" }`

- **Login User**
  - POST `/api/auth/login`
  - Body: `{ "email": "string", "password": "string" }`

### Blog Posts
- **Create Post**
  - POST `/api/posts`
  - Headers: `x-auth-token: <token>`
  - Body: `{ "title": "string", "content": "string" }`

- **Get All Posts**
  - GET `/api/posts`

- **Get Single Post**
  - GET `/api/posts/:id`

- **Update Post**
  - PUT `/api/posts/:id`
  - Headers: `x-auth-token: <token>`
  - Body: `{ "title": "string", "content": "string" }`

- **Delete Post**
  - DELETE `/api/posts/:id`
  - Headers: `x-auth-token: <token>`

### Comments
- **Add Comment**
  - POST `/api/comments`
  - Headers: `x-auth-token: <token>`
  - Body: `{ "content": "string", "postId": "number" }`

- **Get Post Comments**
  - GET `/api/comments/post/:postId`

- **Delete Comment**
  - DELETE `/api/comments/:id`
  - Headers: `x-auth-token: <token>`

## Authentication

The API uses JWT (JSON Web Tokens) for authentication. To access protected routes, you need to:
1. Register or login to get a token
2. Include the token in the request header: `x-auth-token: <your-token>`

## Error Handling

The API returns appropriate HTTP status codes and error messages:
- 200: Success
- 400: Bad Request
- 401: Unauthorized
- 404: Not Found
- 500: Server Error

## Development

To run the application in development mode with auto-reload:
```bash
npm install nodemon --save-dev
npx nodemon src/server.js
```

## Project Structure
```
├── src/
│   ├── config/
│   │   └── db.js          # Database configuration
│   ├── middleware/
│   │   └── auth.js        # Authentication middleware
│   ├── routes/
│   │   ├── auth.js        # Authentication routes
│   │   ├── posts.js       # Blog post routes
│   │   └── comments.js    # Comment routes
│   └── server.js          # Main application file
├── test/
│   └── routes/            # API endpoint tests
├── database.sql           # Database schema
└── package.json
```

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request