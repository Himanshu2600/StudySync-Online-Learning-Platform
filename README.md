# StudySync — Online Learning & Collaboration Platform
A full-stack collaborative learning platform with real-time features, file sharing, polls, and secure authentication.

🚀 Features
💬 Real-time Chat (Socket.io)

Instant message sending and receiving
Typing indicators
Message history on load with auto-scroll
Connection status indicator (green WiFi icon)
Auto-reconnection on disconnect

🟢 Online Status Tracking

Real-time online/offline tracking per group
Online member count in group header
Automatic status updates when users join/leave

📁 File Upload

Upload files up to 50MB
Supports all file types
File metadata display (name, size, type, uploader)
Download functionality
Upload progress via state

📊 Polls & Quizzes

Create polls with multiple options
Dynamic option addition/removal
Vote on polls (one vote per user)
Real-time vote counts and percentage display
Visual progress bars
Poll expiration support

🔔 Real-time Notifications

New messages
New resources
New tasks
Task status changes

🔐 Password Reset

Email-based password reset with secure token
Token expiration after 1 hour
One-time use tokens
Passwords hashed with bcrypt
Toast notifications (no browser alerts)
Auto-redirect after successful reset


🛠️ Tech Stack
LayerTechnologyFrontendReact, ViteBackendNode.js, ExpressDatabaseMongoDB (Mongoose)Real-timeSocket.ioFile UploadMulterAuthJWT, bcryptEmailNodemailer


📁 Project Structure
studysync/
├── server/
│   ├── socket/
│   │   └── socket-handler.js       ← Socket.io server handler
│   ├── models/
│   │   ├── GroupFile.js             ← File upload model
│   │   ├── GroupPoll.js             ← Poll model
│   │   └── PasswordReset.js        ← Password reset token model
│   ├── controllers/
│   │   ├── group-controller.js     ← File upload & poll controllers
│   │   └── auth-controller/
│   │       └── index.js            ← Auth + password reset logic
│   ├── routes/
│   │   ├── group-routes.js         ← File & poll routes
│   │   └── auth-routes/
│   │       └── index.js            ← Auth + reset routes
│   ├── helpers/
│   │   └── email.js                ← Email sending helper
│   └── server.js                   ← Express + Socket.io server
│
└── client/
    ├── src/
    │   ├── hooks/
    │   │   └── useSocket.js        ← Socket.io client hook
    │   ├── pages/
    │   │   ├── auth/
    │   │   │   ├── index.jsx       ← Login + forgot password dialog
    │   │   │   └── reset-password.jsx ← Reset password page
    │   │   └── student/
    │   │       └── groups/
    │   │           └── group-detail.jsx ← Group UI with all features
    │   ├── context/
    │   │   └── auth-context/
    │   │       └── index.jsx       ← Auth context with toast
    │   ├── services/
    │   │   └── index.js            ← API service functions
    │   ├── App.jsx                 ← Routes including reset password
    │   └── main.jsx                ← App entry + Toaster component

⚙️ Setup Instructions
Prerequisites

Node.js >= 16
MongoDB
npm or yarn

1. Clone the Repository
bashgit clone https://github.com/your-username/StudySync-Online-Learning-and-Collaboration-Platform.git
cd StudySync-Online-Learning-and-Collaboration-Platform
2. Configure Server Environment
Create server/.env:
envPORT=5000
MONGO_URI=your_mongodb_uri
CLIENT_URL=http://localhost:5173
JWT_SECRET=your_jwt_secret
INVITE_TOKEN_SECRET=your_invite_secret

# Email (for password reset)
EMAIL_SERVICE=gmail
EMAIL_USER=your-email@gmail.com
EMAIL_PASSWORD=your-16-character-app-password
3. Configure Client Environment
Create client/.env:
envVITE_API_URL=http://localhost:5000
4. Install Dependencies
bash# Install server dependencies
cd server && npm install

# Install client dependencies
cd ../client && npm install
5. Start the Application
Backend:
bashcd server
npm start
Server runs on http://localhost:5000 with Socket.io enabled.
Frontend:
bashcd client
npm run dev
Client runs on http://localhost:5173.

📧 Email Configuration
Gmail (Recommended for Development)

Enable 2-Factor Authentication on your Gmail account
Go to Google Account → Security → 2-Step Verification → App Passwords
Generate an app password for "Mail"
Use the 16-character password in your .env

Production Email Services
ServiceFree TierSendGrid100 emails/dayMailgun5,000 emails/monthPostmark100 emails/monthAWS SESPay as you go
For production, update .env:
envSMTP_HOST=smtp.sendgrid.net
SMTP_PORT=587
EMAIL_USER=apikey
EMAIL_PASSWORD=your-sendgrid-api-key

🧪 Testing Features
Real-time Chat

Open the group page in two different browser tabs
Log in with different accounts
Send messages — they appear instantly in both windows
Observe typing indicators when someone is typing

File Upload

Go to the Files tab in a group
Click Choose File and select any file (max 50MB)
Click Upload File
File appears in the list immediately
Click Download to retrieve files

Polls

Go to the Polls tab
Enter a question and at least 2 options
Click Create Poll
Vote by clicking an option
See real-time vote counts and percentages

Password Reset

Go to /auth and click Forgot password?
Enter your email address
Check your inbox and click the reset link
Enter a new password and confirm
Sign in with your new password


💻 Code Examples
Real-time Chat Hook
javascriptconst { socket, isConnected } = useSocket(groupId);

// Send message
socket?.emit("send-message", { groupId, text: "Hello!" });

// Listen for messages
socket?.on("new-message", (data) => {
  setMessages(prev => [...prev, data.message]);
});
File Upload
javascriptconst formData = new FormData();
formData.append("file", file);
formData.append("description", "File description");

await uploadGroupFileService(groupId, formData);
Create Poll
javascriptawait createGroupPollService(groupId, {
  question: "When can we meet?",
  options: ["Monday", "Tuesday", "Wednesday"],
  expiresAt: "2025-12-31"
});

🔒 Security Features

JWT-based authentication
Password hashing with bcrypt
Password reset tokens expire after 1 hour
One-time use reset tokens
Email format validation
Minimum 6-character password requirement
No email disclosure on reset requests


🛣️ Roadmap
FeatureStatusReal-time Chat✅ CompleteOnline Status✅ CompleteFile Upload✅ CompletePolls/Quizzes✅ CompleteNotifications✅ CompletePassword Reset✅ CompleteVoice/Video Rooms⏳ PlannedShared Whiteboard⏳ PlannedMobile App⏳ Planned

🐛 Troubleshooting
Socket.io Not Connecting

Verify server is running on port 5000
Check VITE_API_URL in client .env
Check browser console for connection errors
Ensure JWT token is valid

File Upload Fails

Confirm file size is under 50MB
Verify uploads/groups directory exists on the server
Check server logs for errors

Polls Not Working

Ensure at least 2 options are provided
Verify MongoDB connection is active
Confirm the user is a group member

Email Not Sending

Check .env has correct email credentials
For Gmail, use an App Password, not your regular password
Check spam/junk folder
Review server logs for SMTP errors


📄 License
This project is licensed under the MIT License.
