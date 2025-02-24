# FastAPI Docker Setup

This guide walks you through setting up and running a FastAPI application using Docker.

## 🛠 Prerequisites

- **Python** (3.7+)
- **FastAPI** and **Uvicorn**
- **Docker** installed and running

---

## 📂 Project Structure

```
api/
│-- app/
│   ├── main.py  # FastAPI application
│-- Dockerfile
│-- requirements.txt
│-- .dockerignore
```

---

## 📜 Step 1: Create and Activate a Virtual Environment

```sh
python -m venv .venv
source .venv/bin/activate  # On Mac/Linux
.venv\Scripts\activate     # On Windows
```

---

## 📦 Step 2: Install Dependencies

```sh
pip install fastapi uvicorn
pip freeze > requirements.txt
```

---

## 📝 Step 3: Write the FastAPI Application

Create `main.py` inside the `app/` directory:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Hello, FastAPI!"}
```

---

## 📄 Step 4: Create the Dockerfile

```Dockerfile
# Use official Python image
FROM python:3.9

# Set working directory
WORKDIR /app

# Copy files
COPY requirements.txt .
COPY app/ ./app

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Expose port
EXPOSE 8000

# Run FastAPI with Uvicorn
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
```

---

## 📂 Step 5: Create a `.dockerignore` File

```plaintext
__pycache__/
.vscode/
.venv/
.DS_Store
*.pyc
```

---

## 🛠 Step 6: Build and Run the Docker Container

### 🔨 Build the Docker Image
```sh
docker build -t my-fastapi-app .
```

### 🚀 Run the Container
```sh
docker run -d -p 8000:8000 my-fastapi-app
```

### 📌 Verify Running Containers
```sh
docker ps
```

---

## 🔍 Step 7: Test the API

### 🏠 Open in Browser
Go to: [http://127.0.0.1:8000](http://127.0.0.1:8000)

### 📑 Access API Docs
- Swagger UI: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)
- Redoc: [http://127.0.0.1:8000/redoc](http://127.0.0.1:8000/redoc)

---

## 🛑 Stopping and Removing the Container

### ❌ Stop Container
```sh
docker stop <container_id>
```

### 🗑 Remove Container
```sh
docker rm <container_id>
```

### 🏷 Remove Image
```sh
docker rmi my-fastapi-app
```

---

## 🎯 Troubleshooting

- **Port Already in Use**
  ```sh
  netstat -ano | findstr :8000  # Find process using port 8000
  taskkill /PID <PID> /F        # Kill process using the port
  ```

- **Container Name Already in Use**
  ```sh
docker rm -f fastapi-app  # Remove existing container
  ```

---

## 🎉 Conclusion
You’ve successfully built and deployed a FastAPI application using Docker! 🚀

