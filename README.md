# LanguageGo

LanguageGo is a full-stack language learning and scoring platform with a **Java backend** and a **Node.js frontend**.  
It provides REST APIs for tracking scores, updating user metadata, and persisting structured data in **Firebase**.  
The frontend communicates with the backend to provide a responsive learning experience.

---

## Table of Contents

- [Demo](#-demo)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Prerequisites](#-prerequisites)
- [Project Structure](#-project-structure)
- [Installation & Setup](#️-installation--setup)
  - [Backend Setup](#1-backend-setup-java--maven)
  - [Frontend Setup](#2-frontend-setup-nodejs)
- [Configuration](#-configuration)
- [Running the Project](#-running-the-project)
- [API Documentation](#-api-documentation)
- [Testing](#-testing)
- [Deployment](#-deployment)
- [Contributing](#-contributing)
- [License](#-license)

---

## Demo

[![Watch Demo](demo.png)](https://drive.google.com/file/d/1Kl2T35G-lxQvuMdP5mCPOLwvyQJm-Hqz/view?usp=sharing)

---

## Features

- RESTful backend in Java (Maven-managed).
- Handlers for:
  - Storing and retrieving scores
  - Updating tags/labels
- Firebase integration for persistent storage.
- JSON and GeoJSON parsing utilities.
- Node.js frontend (npm-based).
- Configurable via environment variables.

---

## Tech Stack

- **Backend:** Java 17+, Maven  
- **Frontend:** Node.js 18+  
- **Database:** Firebase (Firestore/Realtime DB depending on configuration)  
- **Build Tools:** Maven, npm  
- **Version Control:** Git + GitHub  

---

## Prerequisites

Ensure you have the following installed:

- [Java 17+](https://adoptopenjdk.net/)  
- [Maven 3.8+](https://maven.apache.org/)  
- [Node.js 18+ & npm](https://nodejs.org/)  
- Firebase Project (Service Account credentials JSON file)

---

## Project Structure

```
LanguageGo/
├── package.json                # Frontend dependencies
├── package-lock.json
├── server/
│   ├── pom.xml                 # Maven configuration
│   ├── run                     # Script to start backend
│   ├── TODO.md                 # Development notes
│   ├── config/                 # Style configs
│   └── src/main/java/edu/brown/cs/student/main/server/
│       ├── Server.java         # Main server entry point
│       ├── Handlers/           # API request handlers
│       │   ├── GetScoreHandler.java
│       │   ├── StoreScoreHandler.java
│       │   ├── UpdateTagHandler.java
│       │   └── Utils.java
│       └── storage/            # Storage utilities
│           ├── StorageInterface.java
│           ├── FirebaseUtilities.java
│           ├── JSONParser.java
│           └── GeoJsonObject.java
```

---

## Installation & Setup

### 1. Backend Setup (Java + Maven)

```bash
cd server
mvn clean install
./run
```

This builds the backend and launches the server (default port: 8080).

### 2. Frontend Setup (Node.js)

```bash
npm install
npm start
```

This starts the frontend on http://localhost:3000 (by default).

---

## Configuration

The backend requires Firebase credentials and runtime configurations.

Create a `.env` file in the `server/` directory with:

```env
FIREBASE_PROJECT_ID=your-project-id
FIREBASE_CLIENT_EMAIL=your-service-account@your-project.iam.gserviceaccount.com
FIREBASE_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----\nABC...\n-----END PRIVATE KEY-----\n"
SERVER_PORT=8080
```

For the frontend, environment variables can be placed in `.env` at the project root:

```env
REACT_APP_API_BASE_URL=http://localhost:8080
```

---

## Running the Project

**Backend:**

```bash
cd server
./run
```

**Frontend:**

```bash
npm start
```

The app should now be running with:
- Frontend → http://localhost:3000
- Backend API → http://localhost:8080

---

## API Documentation

### GET /score

Retrieve the current score.

**Response:**
```json
{
  "userId": "abc123",
  "score": 42
}
```

### POST /score

Store or update a user score.

**Request:**
```json
{
  "userId": "abc123",
  "score": 50
}
```

**Response:**
```json
{ "status": "success" }
```

### POST /tag/update

Update a user tag.

**Request:**
```json
{
  "userId": "abc123",
  "tag": "grammar"
}
```

**Response:**
```json
{ "status": "updated" }
```

---

## Testing

### Backend Tests

```bash
cd server
mvn test
```

### Frontend Tests

```bash
npm test
```

Made with <3
