# MiterChat

## Project Overview
MiterChat is a real-time chat application that allows users to sign up, log in, update their profiles, and exchange messages with other users. The application supports text and image messages and provides a user-friendly interface for seamless communication.

## Backend Architecture

### Server Setup
The backend is built with Node.js and Express. It uses MongoDB with Mongoose for data storage. The server handles authentication, messaging, and serves the frontend in production.

### API Endpoints

- **Authentication Routes** (`/api/auth`)
  - `POST /signup`: Register a new user.
  - `POST /login`: Authenticate a user.
  - `POST /logout`: Log out the user.
  - `GET /checkAuth`: Check if the user is authenticated.
  - `PUT /updateProfile`: Update user profile picture.

- **Message Routes** (`/api/messages`)
  - `GET /sidebarUsers`: Get list of users for sidebar (excluding logged-in user).
  - `GET /:id`: Get messages between logged-in user and user with specified id.
  - `POST /:id`: Send a message to user with specified id.

### Data Models

- **User**
  - `email` (String, unique, required)
  - `fullName` (String, required)
  - `password` (String, required, min length 6)
  - `profilePic` (String, optional)
  - Timestamps for creation and update

- **Message**
  - `senderId` (ObjectId ref to User, required)
  - `receiverId` (ObjectId ref to User, required)
  - `text` (String, optional)
  - `image` (String, optional)
  - Timestamps for creation and update

### Middleware and Utilities
- Uses middleware for JSON parsing, cookie parsing, and CORS.
- Utilizes Cloudinary for image uploads.
- Implements socket.io for real-time messaging.

## Frontend Architecture

### Main Pages and Routing
- **HomePage**: Main chat interface shown after login.
- **LoginPage**: User login form.
- **SignUpPage**: User registration form.
- **SettingsPage**: User settings.
- **ProfilePage**: User profile view and update.

Routing is handled with `react-router-dom` with protected routes based on authentication state.

### State Management
Uses Zustand for managing authentication state, chat state, and theme preferences.

### Key Components
- **Navbar**: Navigation bar with links and user info.
- **Sidebar**: Displays list of users to chat with.
- **ChatContainer**: Main chat window showing messages.
- **MessageInput**: Input field for sending messages.
- **ChatHeader**: Displays chat partner info.
- **Skeletons**: Loading placeholders for UI elements.

## Features

### Authentication Flow
- Users can sign up with full name, email, and password.
- Passwords are hashed before storage.
- JWT tokens are used for session management via cookies.
- Users can log in, log out, and check authentication status.
- Profile pictures can be updated and are stored via Cloudinary.

### Messaging Flow
- Users can see a list of other users to chat with.
- Messages can be sent as text or images.
- Messages are stored in MongoDB.
- Real-time updates are pushed via socket.io.

## Technologies Used
- Backend: Node.js, Express, MongoDB, Mongoose, bcryptjs, Cloudinary, socket.io
- Frontend: React, react-router-dom, Zustand, Tailwind CSS, lucide-react, react-hot-toast
- Development: Vite, ESLint, PostCSS

## How to Run the Project

### Backend
1. Navigate to the `backend` directory.
2. Install dependencies: `npm install`
3. Create a `.env` file with necessary environment variables (e.g., PORT, MongoDB URI, Cloudinary credentials).
4. Start the server: `npm start` or `node src/index.js`

### Frontend
1. Navigate to the `frontend` directory.
2. Install dependencies: `npm install`
3. Start the development server: `npm run dev`
4. Open the app in the browser at `http://localhost:5173`

## License
This project is licensed under the MIT License.
