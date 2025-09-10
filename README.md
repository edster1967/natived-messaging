# Natived Messaging App

A full-stack social messaging application built with the MEAN stack (MongoDB, Express.js, Angular, Node.js). Users can create accounts, authenticate securely, and share posts with images in a modern, responsive interface.

![MEAN Stack](https://img.shields.io/badge/Stack-MEAN-green)
![Angular](https://img.shields.io/badge/Angular-6.1.10-red)
![Node.js](https://img.shields.io/badge/Node.js-22.19.0-green)
![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-brightgreen)
![Status](https://img.shields.io/badge/Status-Production%20Ready-success)

## 📱 What This App Does

**Natived Messaging** is a social media platform that allows users to:

- 🔐 **User Authentication**: Secure signup and login with JWT tokens
- 📝 **Create Posts**: Share text content with image uploads
- 🖼️ **Image Management**: Upload and display images with posts
- 👥 **User Management**: View and manage user profiles
- 🔒 **Security**: Password hashing with bcrypt and JWT-based authentication
- 📱 **Responsive Design**: Modern Angular Material UI that works on all devices

### Key Features:
- **Real-time Updates**: Dynamic post creation and management
- **Secure Authentication**: JWT tokens with 1-hour expiration
- **File Uploads**: Support for image uploads with posts
- **Cloud Database**: MongoDB Atlas integration for scalability
- **Modern UI**: Angular Material components for professional appearance

---

## 🛠️ Technology Stack

### Frontend
- **Angular 6.1.10** - Modern web framework
- **Angular Material 6.0.2** - UI component library
- **TypeScript 2.7.2** - Strongly typed JavaScript
- **RxJS 6.0.0** - Reactive programming library

### Backend
- **Node.js 22.19.0** - JavaScript runtime
- **Express.js 4.16.3** - Web application framework
- **Mongoose 5.2.14** - MongoDB object modeling
- **JWT (jsonwebtoken 8.3.0)** - Authentication tokens
- **bcryptjs 2.4.3** - Password hashing
- **multer 1.4.4** - File upload handling

### Database & Cloud
- **MongoDB Atlas** - Cloud database service
- **MongoDB** - NoSQL document database

### Development Tools
- **Angular CLI 6.0.8** - Command line interface
- **nodemon 1.18.4** - Development server with auto-restart
- **Karma & Jasmine** - Testing framework

---

## 🗄️ MongoDB Atlas Setup Requirements

Before running the application, you need to set up MongoDB Atlas (cloud database):

### 1. Create MongoDB Atlas Account
1. Visit [MongoDB Atlas](https://www.mongodb.com/atlas)
2. Sign up for a free account
3. Create a new project (e.g., "natived-messaging")

### 2. Create Database Cluster
1. Create a **free M0 cluster**
2. Choose your preferred cloud provider and region
3. Wait for cluster provisioning (1-3 minutes)

### 3. Configure Database Access
1. **Create Database User**:
   - Username: `mtdenatividad_db_user` (or your choice)
   - Password: Strong password (save this!)
   - Privileges: Atlas admin or Read/Write to any database

2. **Set Network Access**:
   - Add your current IP address
   - For development: Add `0.0.0.0/0` (allows access from anywhere)

### 4. Get Connection String
1. Click "Connect" on your cluster
2. Choose "Connect your application"
3. Select Node.js driver
4. Copy the connection string (looks like):
   ```
   mongodb+srv://username:password@cluster0.xxxxx.mongodb.net/natived-messaging?retryWrites=true&w=majority
   ```

### 5. Environment Configuration
Update the `nodemon.json` file with your credentials:
```json
{
    "env": {
        "MONGO_ATLAS_PW": "your_database_password",
        "JWT_KEY": "your_generated_jwt_secret_key"
    }
}
```

**Generate JWT Key** using Node.js:
```bash
node -e "console.log(require('crypto').randomBytes(64).toString('hex'))"
```

### 6. Update Connection String
In `backend/app.js`, replace the MongoDB connection URL with your real Atlas connection string.

---

## 🚀 Local Development Setup

### Prerequisites
- **Node.js v22.19.0** (with `--openssl-legacy-provider` support)
- **npm** package manager
- **MongoDB Atlas account** and cluster (see setup above)

### Installation Steps

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd natived-messaging
   ```

2. **Install dependencies**:
   ```bash
   npm install --legacy-peer-deps
   ```

3. **Configure environment variables**:
   - Update `nodemon.json` with your MongoDB credentials
   - Update `backend/app.js` with your Atlas connection string

4. **Start the backend server**:
   ```bash
   npm run start:server
   ```
   You should see:
   ```
   ✅ Connected to MongoDB Atlas successfully!
   🗄️ Database: natived-messaging
   ```

5. **Start the frontend development server**:
   ```bash
   npm start
   ```
   You should see:
   ```
   ** Angular Live Development Server is listening on localhost:4200 **
   ```

6. **Access the application**:
   - Frontend: http://localhost:4200
   - Backend API: http://localhost:3000

### Available Scripts

```bash
# Start Angular development server
npm start

# Start Node.js backend server  
npm run start:server

# Build for production
npm run build

# Run tests
npm test

# Run e2e tests
npm run e2e

# Lint code
npm run lint
```

---

## 📁 Project Structure

```
natived-messaging/
├── src/                          # Angular frontend source
│   ├── app/                      # Angular application
│   │   ├── auth/                 # Authentication module
│   │   ├── posts/                # Posts management module
│   │   ├── header/               # Navigation header
│   │   └── error/                # Error handling
│   └── environments/             # Environment configurations
├── backend/                      # Node.js backend
│   ├── controllers/              # Route controllers
│   │   ├── posts.js              # Posts API logic
│   │   └── user.js               # User authentication logic
│   ├── models/                   # Mongoose models
│   │   ├── post.js               # Post schema
│   │   └── user.js               # User schema
│   ├── routes/                   # Express routes
│   ├── middleware/               # Custom middleware
│   ├── images/                   # Uploaded images storage
│   ├── app.js                    # Express app configuration
│   └── server.js                 # Server startup
├── nodemon.json                  # Environment variables
└── package.json                  # Dependencies and scripts
```

---

## 🔧 API Endpoints

### Authentication
- `POST /api/user/signup` - Create new user account
- `POST /api/user/login` - User login with JWT token

### Posts Management
- `GET /api/posts` - Get all posts
- `POST /api/posts` - Create new post (requires authentication)
- `PUT /api/posts/:id` - Update post (requires authentication)
- `DELETE /api/posts/:id` - Delete post (requires authentication)

### File Upload
- Images are uploaded with posts and stored in `/backend/images/`

---

## 🔒 Security Features

- **Password Hashing**: bcrypt with 10 salt rounds
- **JWT Authentication**: Secure token-based authentication
- **Route Protection**: Middleware to protect authenticated routes
- **Input Validation**: Server-side validation for all inputs
- **CORS Configuration**: Proper cross-origin resource sharing setup

---

## 🚀 Deployment

### Environment Variables (Production)
```bash
MONGODB_URI=your_full_atlas_connection_string
JWT_KEY=your_secure_jwt_secret
NODE_OPTIONS=--openssl-legacy-provider
```

### Build for Production
```bash
# Build Angular app
npm run build

# Start production server
node backend/server.js
```

---

## 🐛 Known Issues & Solutions

### MongoDB Connection Warnings
- **Issue**: Deprecation warnings from MongoDB driver
- **Status**: Non-critical - application functions correctly
- **Solution**: Will be resolved in future MongoDB driver updates

### Missing Image Files
- **Issue**: ENOENT errors for missing image files
- **Cause**: References to uploaded images that don't exist
- **Solution**: Upload test images or implement graceful error handling

### Node.js Compatibility
- **Requirement**: Use `--openssl-legacy-provider` flag for Node.js 17+
- **Reason**: Angular 6 webpack compatibility with modern Node.js versions

---

## 📝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License.

---

## 🆘 Support

If you encounter issues:

1. **Check MongoDB Connection**: Verify Atlas cluster is active and credentials are correct
2. **Verify Environment Variables**: Ensure `nodemon.json` has correct values
3. **Check Dependencies**: Run `npm install --legacy-peer-deps` if needed
4. **Review Console Logs**: Both frontend and backend provide detailed error messages

### Helpful Commands
```bash
# Reset dependencies
rm -rf node_modules package-lock.json
npm install --legacy-peer-deps

# Check server status
npm run start:server

# Check connection to MongoDB
# Look for: "✅ Connected to MongoDB Atlas successfully!"
```

---

*Last Updated: September 10, 2025*
