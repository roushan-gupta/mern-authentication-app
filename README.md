# MERN Authentication Mobile App

A complete full-stack authentication application built with **MongoDB**, **Express**, **React Native (Expo)**, and **Node.js** (MERN stack).

This project demonstrates a production-ready authentication system with JWT tokens, secure password hashing, protected routes, and a beautiful mobile UI.

## Features

- User registration and login
- JWT token-based authentication
- Secure password hashing with bcryptjs
- Protected routes and API endpoints
- AsyncStorage for persistent sessions
- Clean, modern, responsive UI
- Form validation and error handling
- Automatic token refresh and authentication checks

## Tech Stack

### Backend
- **Node.js** - JavaScript runtime
- **Express.js** - Web framework
- **MongoDB** - NoSQL database
- **Mongoose** - MongoDB ODM
- **bcryptjs** - Password hashing
- **jsonwebtoken** - JWT authentication
- **CORS** - Cross-origin resource sharing
- **dotenv** - Environment variable management

### Frontend
- **React Native** - Mobile framework
- **Expo** - Development platform
- **Expo Router** - File-based navigation
- **TypeScript** - Type safety
- **Axios** - HTTP client
- **AsyncStorage** - Local data persistence
- **Lucide Icons** - Modern icon library

## Project Structure

```
Main Folder/
├── backend/                    # Backend server
│   ├── config/
│   │   └── db.js              # MongoDB connection
│   ├── middleware/
│   │   └── auth.js            # JWT authentication middleware
│   ├── models/
│   │   └── User.js            # User model schema
│   ├── routes/
│   │   └── auth.js            # Authentication routes
│   ├── .env                   # Environment variables
│   ├── .env.example           # Example environment variables
│   ├── package.json           # Backend dependencies
│   ├── server.js              # Main server entry point
│   └── README.md              # Backend documentation
│
└── frontend/                   # React Native app
    ├── app/
    │   ├── _layout.tsx        # Root layout
    │   ├── index.tsx          # Entry point
    │   ├── login.tsx          # Login screen
    │   ├── register.tsx       # Register screen
    │   ├── dashboard.tsx      # Dashboard screen (protected)
    │   └── +not-found.tsx     # 404 screen
    ├── context/
    │   └── AuthContext.tsx    # Authentication context
    ├── services/
    │   └── api.ts             # API service with axios
    ├── hooks/
    │   └── useFrameworkReady.ts
    ├── types/
    │   └── env.d.ts           # Environment type definitions
    ├── assets/                # Images and assets
    ├── .env                   # Frontend environment variables
    ├── app.json               # Expo configuration
    ├── package.json           # Frontend dependencies
    └── tsconfig.json          # TypeScript configuration
```

## Getting Started

### Prerequisites

- **Node.js** (v16 or higher)
- **npm** or **yarn**
- **MongoDB Atlas account** (free tier available)
- **Expo Go app** on your phone (for testing)

### Step 1: Clone the Repository

```bash
git clone <repository-url>
cd mern-auth-app
```

### Step 2: Setup Backend

1. Navigate to backend folder:
```bash
cd backend
```

2. Install dependencies:
```bash
npm install
```

3. Create `.env` file:
```bash
cp .env.example .env
```

4. Update `.env` with your MongoDB connection string:
```env
PORT=5000
MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/authDB?retryWrites=true&w=majority
JWT_SECRET=your_very_strong_secret_key_here
```

**To get MongoDB URI:**
- Go to [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
- Create a free cluster
- Click "Connect" > "Connect your application"
- Copy the connection string
- Replace `<password>` with your database password

5. Start the backend server:
```bash
npm start
```

The server will run on `http://localhost:5000`

### Step 3: Setup Frontend

1. Open a new terminal and navigate to frontend folder:
```bash
cd frontend
```

2. Install dependencies:
```bash
npm install
```

3. Update `.env` file with your backend URL:
```env
EXPO_PUBLIC_API_URL=http://localhost:5000
```

**Important:** If testing on a physical device, replace `localhost` with your computer's IP address:
```env
EXPO_PUBLIC_API_URL=http://192.168.1.100:5000
```

4. Start the Expo development server:
```bash
npm run dev
```

5. Scan the QR code with:
- **iOS:** Camera app
- **Android:** Expo Go app

## API Endpoints

### Base URL
```
http://localhost:5000/api/auth
```

### 1. Register User
**POST** `/api/auth/register`

**Request Body:**
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "password123"
}
```

**Response:**
```json
{
  "success": true,
  "message": "User registered successfully",
  "user": {
    "id": "user_id",
    "name": "John Doe",
    "email": "john@example.com",
    "createdAt": "2024-01-01T00:00:00.000Z"
  }
}
```

### 2. Login User
**POST** `/api/auth/login`

**Request Body:**
```json
{
  "email": "john@example.com",
  "password": "password123"
}
```

**Response:**
```json
{
  "success": true,
  "message": "Login successful",
  "token": "jwt_token_here",
  "user": {
    "id": "user_id",
    "name": "John Doe",
    "email": "john@example.com",
    "createdAt": "2024-01-01T00:00:00.000Z"
  }
}
```

### 3. Get Current User (Protected)
**GET** `/api/auth/me`

**Headers:**
```
Authorization: Bearer your_jwt_token_here
```

**Response:**
```json
{
  "success": true,
  "user": {
    "id": "user_id",
    "name": "John Doe",
    "email": "john@example.com",
    "createdAt": "2024-01-01T00:00:00.000Z"
  }
}
```

## How It Works

### Authentication Flow

1. **Registration:**
   - User fills in name, email, and password
   - Password is hashed using bcryptjs
   - User is saved to MongoDB
   - User is auto-logged in

2. **Login:**
   - User enters email and password
   - Password is compared with hashed password
   - JWT token is generated and sent to client
   - Token and user data are stored in AsyncStorage

3. **Protected Routes:**
   - Token is automatically attached to all API requests
   - Backend middleware verifies token
   - If valid, user data is attached to request
   - If invalid, 401 error is returned

4. **Logout:**
   - Token and user data are removed from AsyncStorage
   - User is redirected to login screen

### Security Features

- Passwords are hashed using bcryptjs (salt rounds: 10)
- JWT tokens expire after 7 days
- Protected routes require valid JWT token
- Tokens are automatically refreshed
- Secure HTTP-only cookie support (can be added)
- Input validation and sanitization
- Error handling and logging

## Screens

### 1. Login Screen
- Email and password inputs
- Form validation
- Error handling
- Link to registration

### 2. Register Screen
- Name, email, password, and confirm password inputs
- Password strength validation
- Email format validation
- Auto-login after registration

### 3. Dashboard Screen (Protected)
- User profile information
- Account status cards
- Feature highlights
- Logout functionality
- Responsive layout

## Testing the App

### Using Expo Go App

1. Install Expo Go on your phone:
   - [iOS App Store](https://apps.apple.com/app/expo-go/id982107779)
   - [Google Play Store](https://play.google.com/store/apps/details?id=host.exp.exponent)

2. Make sure your phone and computer are on the same WiFi network

3. Scan the QR code from the terminal

4. The app will load on your phone

### Using Web Browser

```bash
cd frontend
npm run dev
```

Press `w` to open in web browser.

## Common Issues & Solutions

### Backend Issues

**MongoDB Connection Error:**
- Verify your connection string is correct
- Check if your IP is whitelisted in MongoDB Atlas
- Ensure database user has proper permissions

**Port Already in Use:**
- Change PORT in `.env` file
- Or kill the process: `lsof -ti:5000 | xargs kill`

### Frontend Issues

**Cannot Connect to Backend:**
- Make sure backend server is running
- Update `EXPO_PUBLIC_API_URL` with correct IP address
- Check firewall settings

**QR Code Not Scanning:**
- Ensure you're using Expo Go app (not camera)
- Try typing the URL manually in Expo Go

## Development Tips

- Use `console.log()` for debugging
- Check Network tab in browser DevTools
- Use Postman or Thunder Client to test API
- Enable React DevTools for debugging
- Use TypeScript for better code quality

## Deployment

### Backend Deployment

**Recommended Platforms:**
- Railway
- Render
- Heroku
- DigitalOcean

**Steps:**
1. Set environment variables on hosting platform
2. Update MongoDB whitelist to allow all IPs (0.0.0.0/0)
3. Deploy backend code
4. Get the deployed URL

### Frontend Deployment

**For Web:**
```bash
cd frontend
npm run build:web
```

**For Mobile:**
- Build APK/IPA using EAS Build
- Submit to App Store / Play Store

**Update API URL:**
```env
EXPO_PUBLIC_API_URL=https://your-backend-url.com
```

## Contributing

This project is built for learning purposes. Feel free to:
- Fork the repository
- Create feature branches
- Submit pull requests
- Report issues

## License

MIT License - feel free to use this project for learning and portfolio purposes.

## Support

If you encounter any issues or have questions:
1. Check the README documentation
2. Review the inline code comments
3. Check console logs for errors
4. Open an issue on GitHub

## Acknowledgments

- Built with love for learning and demonstration
- Perfect for fresher job applications
- Demonstrates full-stack development skills
- Production-ready code structure

---

**Happy Coding!** 🚀
