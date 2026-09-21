# 💬 Real-Time Chat Application

A full-stack real-time chat application built with Next.js, React, Node.js, TypeScript, Express.js, Socket.IO, RabbitMQ, Redis, MongoDB, JWT, OTP authentication, Docker, PM2, and AWS EC2.

## 🚀 Features

- User registration and login
- JWT-based authentication
- OTP-based email verification
- OTP expires after 5 minutes
- OTP request rate limiting
- Secure password authentication
- Protected routes
- Real-time one-to-one messaging
- Socket.IO-based communication
- Instant message delivery
- User search
- Chat selection
- Persistent chat messages
- RabbitMQ-based asynchronous email processing
- Gmail SMTP integration using Nodemailer
- Redis-based OTP rate limiting
- MongoDB for persistent data storage
- MongoDB Atlas cloud database
- Docker-based infrastructure
- PM2 process management
- AWS EC2 deployment
- Linux server deployment

## 🏗️ Architecture
                         ┌─────────────────────┐
                         │      Frontend       │
                         │      Next.js        │
                         └──────────┬──────────┘
                                    │
                          HTTP / WebSocket
                                    │
                                    ▼
                ┌──────────────────────────────────┐
                │             Backend              │
                │                                  │
                │  ┌────────────────────────────┐  │
                │  │       User Service         │  │
                │  │  Authentication / JWT      │  │
                │  │  OTP Verification          │  │
                │  └─────────────┬──────────────┘  │
                │                │                 │
                │                ▼                 │
                │             MongoDB              │
                │                                  │
                │  ┌────────────────────────────┐  │
                │  │       Chat Service         │  │
                │  │       Socket.IO            │  │
                │  │       Messaging            │  │
                │  └─────────────┬──────────────┘  │
                │                │                 │
                │                ▼                 │
                │              Redis               │
                │                                  │
                │  ┌────────────────────────────┐  │
                │  │       Mail Service         │  │
                │  │       Nodemailer            │  │
                │  └─────────────┬──────────────┘  │
                │                │                 │
                └────────────────┼─────────────────┘
                                 │
                                 ▼
                            RabbitMQ
                                 │
                                 ▼
                           Gmail SMTP
--------------------------------------------------------------------------------------------------------------------------------------------------------------
Technology Stack

Frontend
Next.js
React
TypeScript
Socket.IO Client
CSS
Backend
Node.js
Express.js
TypeScript
Socket.IO
JWT
RabbitMQ
Redis
Nodemailer
Database
MongoDB
MongoDB Atlas
Cloud & DevOps
AWS EC2
Docker
PM2
Linux
Git
GitHub
--------------------------------------------------------------------------------------------------------------------------------------------------------------------
🔐 Authentication Flow

User
 │
 ▼
Frontend
 │
 ▼
User Service
 │
 ├── Validate Credentials
 │
 ├── Generate JWT
 │
 ▼
Frontend
 │
 ▼
Authenticated User

JWT is used to authenticate protected application functionality.
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
📧 OTP Verification Flow

User
 │
 ▼
Frontend
 │
 ▼
User Service
 │
 ├── Generate OTP
 │
 ▼
RabbitMQ
 │
 ▼
Mail Service
 │
 ▼
Gmail SMTP
 │
 ▼
User receives OTP
 │
 ▼
OTP Verification
 │
 ▼
Account Verified
----------------------------------------------------------------------------------------------------------------------------------------------------------------------
OTP Features

OTP generation
OTP email delivery
OTP expires after 5 minutes
OTP request rate limiting
Asynchronous email processing
RabbitMQ message queue
Gmail SMTP
Nodemailer
--------------------------------------------------------------------------------------------------------------------------------------------------------------------
⚡ Redis Rate Limiting

Redis is used to control OTP request frequency.

User Requests OTP
       │
       ▼
     Redis
       │
       ├── Request Allowed
       │        │
       │        ▼
       │    Generate OTP
       │
       └── Request Too Frequent
                │
                ▼
              Reject

Redis provides fast in-memory operations and helps prevent excessive OTP requests.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------
🐇 RabbitMQ

RabbitMQ is used for asynchronous communication between backend services.

Instead of directly sending an email:

User Service ───────► Gmail

the application uses:

User Service
     │
     ▼
 RabbitMQ
     │
     ▼
 Mail Service
     │
     ▼
 Gmail SMTP

This separates OTP request processing from email delivery.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------
💬 Real-Time Messaging

Socket.IO is used for real-time communication.

User A
 │
 │ Socket.IO
 ▼
Chat Service
 │
 ├──────────────────► User B
 │                       │
 │                       ▼
 │                 Real-Time Message
 │
 ▼
MongoDB

The Chat Service manages real-time connections and messaging.
---------------------------------------------------------------------------------------------------------------------------------------------------------------------
🗄️ MongoDB

MongoDB is used as the primary persistent database.

Application data includes:

Users
Chats
Messages
Authentication-related data

MongoDB Atlas provides cloud-hosted MongoDB infrastructure.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------
🔧 Backend Services

User Service
Responsible for:

User registration
User login
Authentication
JWT generation
OTP generation
OTP verification
User information

Chat Service
Responsible for:

Chat functionality
Real-time communication
Socket.IO connections
Message handling
Chat-related operations

Mail Service
Responsible for:

OTP email delivery
RabbitMQ message consumption
Nodemailer
Gmail SMTP communication

---------------------------------------------------------------------------------------------------------------------------------------------------------------------
🌐 Communication Technologies

HTTP
Used for REST API communication and authentication operations.

WebSocket / Socket.IO
Used for real-time messaging and persistent socket connections.

RabbitMQ
Used for asynchronous communication between backend services.

Redis
Used for OTP rate limiting and fast temporary operations.

MongoDB
Used for persistent application data.

---------------------------------------------------------------------------------------------------------------------------------------------------------------------
💻 Local Development
Prerequisites

Install:

Node.js
npm
MongoDB / MongoDB Atlas
Redis
RabbitMQ
Git

👤 User Service .env
Create:
user/.env

Example:

PORT=5000

MONGODB_URI=your_mongodb_connection_string

JWT_SECRET=your_jwt_secret

RABBITMQ_HOST=your_rabbitmq_host
RABBITMQ_USERNAME=your_rabbitmq_username
RABBITMQ_PASSWORD=your_rabbitmq_password

REDIS_URL=your_redis_url

💬 Chat Service .env
Create:
chat/.env

Example:

PORT=your_chat_service_port

MONGODB_URI=your_mongodb_connection_string

JWT_SECRET=your_jwt_secret

REDIS_URL=your_redis_url

📧 Mail Service .env
Create:
mail/.env

Example:

PORT=5001

RABBITMQ_HOST=your_rabbitmq_host
RABBITMQ_USERNAME=your_rabbitmq_username
RABBITMQ_PASSWORD=your_rabbitmq_password

GMAIL_USER=your_email@gmail.com
GMAIL_PASSWORD=your_gmail_app_password
Clone Repository
git clone https://github.com/navin-mk/chatbackend.git
cd chatbackend

Install User Service
cd user
npm install

Install Chat Service
cd ../chat
npm install

Install Mail Service
cd ../mail
npm install

Install Frontend
cd ../frontend
npm install
---------------------------------------------------------------------------------------------------------------------------------------------------------------------
▶️ Running the Application

Start the required infrastructure:

MongoDB
Redis
RabbitMQ
Start User Service
cd user
npm run dev
Start Chat Service
cd chat
npm run dev
Start Mail Service
cd mail
npm run dev
Start Frontend
cd frontend
npm run dev

Frontend:

http://localhost:3000
🏭 Production Build
Frontend
cd frontend
npm install
npm run build
npm start
Backend

Build the TypeScript services:

npm run build

Start the compiled application:

node dist/index.js
🔄 PM2 Deployment

PM2 is used to manage Node.js processes in production.

User Service

pm2 start "node dist/index.js" --name user-service

Chat Service

pm2 start "node dist/index.js" --name chat-service

Mail Service

pm2 start "node dist/index.js" --name mail-service

Frontend

pm2 start npm --name frontend -- run start

Check Services
pm2 list

View Logs
pm2 logs

Save PM2 Processes
pm2 save
--------------------------------------------------------------------------------------------------------------------------------------------------------------------
☁️ AWS EC2 Deployment

                         Internet
                            │
                            ▼
                    ┌───────────────┐
                    │   AWS EC2     │
                    │    Ubuntu     │
                    └───────┬───────┘
                            │
             ┌──────────────┼──────────────┐
             │              │              │
             ▼              ▼              ▼
         Frontend       Backend       Infrastructure
         Next.js        Services
                            │
                  ┌─────────┼─────────┐
                  │         │         │
                  ▼         ▼         ▼
               User      Chat       Mail
              Service   Service    Service
                  │         │         │
                  └─────────┼─────────┘
                            │
                    ┌───────┴────────┐
                    ▼                ▼
                  Redis           RabbitMQ
                                      │
                                      ▼
                                 Gmail SMTP

                         MongoDB Atlas
                              ▲
                              │
                         Backend Services

The application is deployed on an AWS EC2 Ubuntu server.

AWS EC2 hosts the application services and supporting infrastructure.

MongoDB Atlas is used as the cloud database.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------
🐳 Docker

Docker is used to run infrastructure and application components in containers.

Main components include:

RabbitMQ
Redis
Backend services
Frontend

Docker Compose can be used to manage multiple containers together.

🔒 Security

The application implements:

JWT authentication
OTP verification
OTP expiration
OTP rate limiting
Protected routes
Environment variables
Password authentication
Authentication middleware

For production deployments, additional security measures should include:

HTTPS
Secure cookies
Proper CORS configuration
Input validation
Rate limiting
Secret management
Restricted database access
Restricted RabbitMQ access
AWS Security Groups
🔐 Git & Secret Management

The following files should never be committed:

.env
.env.local
*.pem
node_modules/
.next/

Before pushing code:

git status

Always verify that sensitive information is not staged.
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
🧪 Testing
Authentication Testing

Test scenarios include:

User registration
OTP generation
OTP email delivery
Valid OTP verification
Invalid OTP
Expired OTP
Repeated OTP requests
Login
Invalid credentials
Protected route access
Chat Testing

Test scenarios include:

Login with multiple users
Search users
Select a user
Start a conversation
Send messages
Receive messages in real time
Refresh the application
Verify persisted messages

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
Deployment Stack

                         AWS EC2
                            │
             ┌──────────────┼──────────────┐
             │              │              │
             ▼              ▼              ▼
          Next.js       User Service   Chat Service
          Frontend           │              │
                              │              │
                              └──────┬───────┘
                                     │
                              ┌──────┴──────┐
                              │             │
                              ▼             ▼
                            Redis        MongoDB
                              │           Atlas
                              │
                         Rate Limiting

                         Mail Service
                              │
                              ▼
                          RabbitMQ
                              │
                              ▼
                         Gmail SMTP

                         PM2
                          │
                          ▼
                   Process Management
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
🧠 Key Engineering Concepts

This project demonstrates practical experience with:

Full-stack web development
Next.js
React
Node.js
TypeScript
Express.js
REST APIs
WebSockets
Socket.IO
JWT authentication
OTP authentication
RabbitMQ
Redis
MongoDB
MongoDB Atlas
Service-oriented architecture
Asynchronous processing
Rate limiting
Docker
PM2
Linux
AWS EC2
Git
GitHub
Production deployment
----------------------------------------------------------------------------------------------------------------------------------------------------------------------
🔮 Future Improvements

Nginx reverse proxy
HTTPS / SSL
Custom domain
Docker Compose deployment
GitHub Actions CI/CD
Redis Socket.IO adapter
RabbitMQ retry mechanism
RabbitMQ dead-letter queue
Online/offline user status
Typing indicators
Message read receipts
File and image sharing
Push notifications
Prometheus monitoring
Grafana dashboards
Centralized logging
Automated testing
Horizontal scaling

👨‍💻 Author
Navin Mahendran

GitHub: https://github.com/navin-mk

📄 License

This project is developed for educational, learning, and portfolio purposes.
