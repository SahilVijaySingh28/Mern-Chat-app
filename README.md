# My Chat App 💬
A real-time chat application where users can sign up, search for friends, and chat instantly using WebSockets.

**Features:**
- User authentication with JWT
- Real-time messaging with Socket.io
- Search and add users
- Online user status
- Beautiful UI with Tailwind CSS

---

## Tech Stack
- **Frontend:** React.js, Vite, Tailwind CSS, Zustand
- **Backend:** Node.js, Express.js, Socket.io
- **Database:** MongoDB Atlas
- **Containerization:** Docker
- **Orchestration:** Kubernetes, Helm (optional)
- **Infrastructure:** Terraform for AWS

---

## Setup Instructions

### 1. Prerequisites
- Node.js v18+
- MongoDB Atlas account (free tier available)
- Git

### 2. Clone & Install
```bash
git clone https://github.com/YOUR_USERNAME/my-chat-app.git
cd my-chat-app
npm install
cd frontend && npm install && cd ..
```

### 3. Create .env file
Create a `.env` file in the project root:
```
PORT=5000
MONGO_DB_URI=mongodb+srv://your_username:your_password@your_cluster.mongodb.net/chatapp?retryWrites=true&w=majority
JWT_SECRET=your_super_secret_jwt_key_here_make_it_random
NODE_ENV=development
```

### 4. Start the Application

**Development Mode (with auto-reload):**
```bash
# Terminal 1 - Backend
npm run server

# Terminal 2 - Frontend
cd frontend
npm run dev
```

**Production Mode:**
```bash
npm run build
npm start
```

### 5. Access the App
- Frontend: http://localhost:5173
- Backend API: http://localhost:5000

---

## How to Use
1. Sign up with your username, full name, password, and gender
2. Search for another user
3. Start chatting in real-time!
4. See online users and their status

---

## Build & Deploy

### Build the app locally
```shell
npm run build
```

### Docker
```bash
docker build -t your_username/my-chat-app:v1 .
docker run -p 5000:5000 --env-file .env your_username/my-chat-app:v1
```

---

## Project Structure
```
.
├── backend/
│   ├── controllers/
│   ├── models/
│   ├── routes/
│   ├── socket/
│   └── server.js
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── context/
│   │   ├── pages/
│   │   └── App.jsx
│   └── package.json
└── Dockerfile
```

---

## Author
Created by: **Your Name**  
GitHub: [@YOUR_USERNAME](https://github.com/YOUR_USERNAME)

---

## License
This project is open source and available under the MIT License.

## Infrastructure Overview
This project uses the following AWS resources:
- **VPC** with public subnets
- **Internet Gateway** and route tables for public access
- **EKS Cluster** provisioned via Terraform
- **Managed Node Group** (3 x t2.large worker nodes)
- **NGINX Ingress Controller** deployed for routing
- **NodePort Service** for Kubernetes workloads
- **Security Groups** Allowing HTTP/HTTPS, NodePort, and SSH access

## Architecture Diagram
![Architecture Diagram](./images/ArchitectureDiagram.png)

## Tech Stack
- **Frontend**: React.js
- **Backend**: Node.js, Express.js
- **Database**: MongoDB Atlas
- **Infrastructure**: Terraform
- **Containerization**: Docker
- **Orchestration**: Kubernetes
- **CI/CD**: GitHub Actions & ArgoCD
- **Cloud**: AWS
- **Routing**: NGINX Ingress

## Pull the Docker Image
```shell
docker pull abhi0874/chatapp-multistage:v1
```
### Run the container
```shell
docker run chatapp-multistage
``` 

## GitHub Actions CI
![Ci Diagram](./images/CI.png)

## ArgoCD
![Deployment Diagram](./images/DeploymentDiagram.png)
