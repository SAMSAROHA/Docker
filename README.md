# Docker Demo - Node.js Application

This is a comprehensive Docker demonstration project featuring a Node.js Express application with multiple configurations and deployment pipelines.

## 📋 Project Overview

A complete Docker learning project that demonstrates:
- Basic Docker containerization with Node.js
- Docker Compose for multi-container orchestration
- MySQL database integration
- Jenkins CI/CD pipelines
- Vagrant VM configuration
- Automated testing with Mocha

## 📁 Project Structure

```
├── Dockerfile                 # Basic Node.js container image
├── docker-compose.yml         # Multi-container orchestration (web + database)
├── index.js                   # Simple Express.js "Hello World" app
├── index-db.js               # Express.js app with MySQL integration
├── package.json              # Node.js dependencies
├── package-lock.json         # Locked dependency versions
├── README.md                 # Project documentation
├── test/
│   └── test.js              # Mocha test suite
└── misc/
    ├── Jenkinsfile          # Jenkins CI/CD pipeline v1
    ├── Jenkinsfile.v2       # Jenkins CI/CD pipeline v2 (with DB testing)
    └── Vagrantfile          # Vagrant VM configuration for Ubuntu
```

## 🚀 Getting Started

### Prerequisites
- Docker & Docker Compose
- Node.js (for local development)
- Git

### Quick Start

#### Option 1: Run with Docker Compose
```bash
# Navigate to project directory
cd Docker

# Start both web and database services
docker-compose up -d

# Access the application
curl http://localhost:3000
```

#### Option 2: Build and Run Manually
```bash
# Build Docker image
docker build -t myapp:latest .

# Run container
docker run -p 3000:3000 myapp:latest
```

#### Option 3: Local Node.js Development
```bash
# Install dependencies
npm install

# Run the application
npm start

# Run tests
npm test
```

## 📝 Application Files

### **index.js**
Simple Express.js server that returns "Hello World!"
- Listens on port 3000
- Single GET route at `/`
- No database dependency

### **index-db.js**
Express.js server with MySQL database integration
- Connects to MySQL database
- Creates `visits` table automatically
- Tracks visitor count with timestamps
- Response: "Hello World! You are visitor number X"

### **package.json**
Dependencies:
- **express**: ^4.14.0 - Web framework
- **http-errors**: ^1.7.0 - HTTP error handling
- **mysql2**: ^3.2.0 - MySQL driver

Dev Dependencies:
- **mocha**: ^5.2.0 - Testing framework
- **inherits**: ^2.0.3 - Utility
- **ms**: ^2.1.1 - Time utilities

## 🐳 Docker Configuration

### **Dockerfile**
```dockerfile
FROM node
WORKDIR /app
ADD . /app
RUN npm install
EXPOSE 3000
CMD ["npm", "start"]
```

### **docker-compose.yml**
Two services:
1. **web**: Node.js application
   - Builds from current directory
   - Runs `index-db.js`
   - Port: 3000:3000
   - Links to `db` service

2. **db**: MySQL database
   - Image: mysql:8
   - Port: 3306:3306
   - Database: myapp
   - User: myapp / Password: mysecurepass
   - Root Password: securerootpass

## 🧪 Testing

Run the test suite:
```bash
npm test
```

Tests are written with Mocha and assert basic functionality.

## 🔄 CI/CD Pipelines

### **Jenkinsfile** (v1)
Basic pipeline for:
1. Checkout source code
2. Run tests with Node.js
3. Build and push Docker image to Docker Hub

### **Jenkinsfile.v2** (Enhanced)
Advanced pipeline with:
1. Preparation stage (git checkout)
2. Unit testing in Docker container
3. Integration testing with MySQL database
4. Docker image build and push

## 💻 Vagrant Configuration

**misc/Vagrantfile** provides Ubuntu development environment:
- Box: ubuntu/trusty64
- Network: Private (192.168.0.249)
- Hostname: docker.example.com

## 🌐 Endpoints

### Simple App (index.js)
- `GET /` → "Hello World!"

### Database App (index-db.js)
- `GET /` → "Hello World! You are visitor number X"
- Increments visitor count on each request
- Stores timestamps in MySQL

## 📊 Database Schema

**visits table** (auto-created):
```sql
CREATE TABLE visits (
  id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
  ts BIGINT
)
```

## 🔧 Environment Variables

For `docker-compose.yml`:
- `MYSQL_DATABASE`: myapp
- `MYSQL_USER`: myapp
- `MYSQL_PASSWORD`: mysecurepass
- `MYSQL_HOST`: db
- `MYSQL_ROOT_PASSWORD`: securerootpass

## 📚 Learning Resources

This project demonstrates:
- ✅ Container basics with Dockerfile
- ✅ Multi-container orchestration with Docker Compose
- ✅ Database integration
- ✅ CI/CD automation with Jenkins
- ✅ Infrastructure as code with Vagrant
- ✅ Automated testing

## 🔗 Related Links

- [Docker Documentation](https://docs.docker.com/)
- [Docker Compose Guide](https://docs.docker.com/compose/)
- [Node.js Docker Best Practices](https://nodejs.org/en/docs/guides/nodejs-docker-webapp/)
- [Express.js Documentation](https://expressjs.com/)
- [MySQL Documentation](https://dev.mysql.com/doc/)

## 📄 License

This project is open source and available for educational purposes.

## 👤 Original Author

Used wardviaene/docker-demo repository For reference

---

**Last Updated**: May 25, 2026
