---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:21
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:15
tags:
  - Docker
  - celery
---
Folder structure  
structure  

```JavaScript
Folder structure
structure
- celery_app
- - app
- - - celery.py
- - celery.Dockerfile
- jd
- - app
- - - main.py
- - - - task
- - - - - task.py (celery task)
- - jd.Dockerfile
- - requirements.txt
```

Notes:

1. don't initialize celery inside app, move into a central location
2. in celery app folder, initialize celery this way `celery.py`

```Plain
from celery import Celery

url = "redis://redis:6379"
celery_app = Celery(
    "app",
    broker=url,
    backend=url,
    include=[
        "cv.app.task.task",
        "jd.app.task.task",
    ]
)

celery_app.autodiscover_tasks()
```

And docker file should contain all the module `celery.Dockerfile`

```Plain
# Use the same base image as your cv.Dockerfile and jd.Dockerfile
FROM python:3.9

# Set the working directory
WORKDIR /app

# Copy the requirements.txt file to the container
COPY ../cv/requirements.txt requirements1.txt
RUN pip install -r requirements1.txt

# Now run JD
COPY ../jd/requirements.txt requirements2.txt
RUN pip install -r requirements2.txt

# Copy the entire cv and jd folders to the container
Copy ../celery_app /app
COPY ../cv /app/cv
COPY ../jd /app/jd

# Set the Celery environment variables
ENV CELERY_BROKER_URL=redis://redis:6379/0
ENV CELERY_RESULT_BACKEND=redis://redis:6379/0

# Add the task module to the Python path
ENV PYTHONPATH=/app

# Define the command to run the Celery worker
CMD celery -A app worker --loglevel=INFO
```

### JD app

1. Normal Fastapi app -> `main.py`

```Plain
from fastapi import FastAPI
from fastapi.responses import ORJSONResponse

app = FastAPI(
    title="FastAPI V1",
    version="1.0.1",
    debug=True,
    # docs_url="/docs",
    swagger_ui_oauth2_redirect_url="/auth/token",
    default_response_class=ORJSONResponse,
)


@app.get("/ping")
async def ping():
    return {"status": "OK"}


@app.get("/v1")
async def ping():
    return {"status": "OK"}

```

1. Define task normally `task.py`

```Plain
from celery import shared_task


@shared_task()
def jd_job():
    print("*************************************")
    print("JD job")
    print("*************************************")
    return {"status": "OK", "res": "add job"}
```

### Docker compose

```Plain
version: "3.9"

services:
  jd:
    build:
      context: jd
      dockerfile: jd.Dockerfile
    container_name: jd
    restart: always
    volumes:
      - ./jd:/app
    command: >
      sh -c "uvicorn app.main:app --reload --host 0.0.0.0 --port 8000 --root-path='/jd'"
    ports:
      - "8000:8000"

  cv:
    build:
      context: cv
      dockerfile: cv.Dockerfile
    container_name: cv
    restart: always
    volumes:
      - ./cv:/app
    command: >
      sh -c "uvicorn app.main:app --reload --host 0.0.0.0 --port 8080 --root-path='/cv'"
    ports:
      - "8080:8080"

  celery:
    build:
      context: .
      dockerfile: celery_app/celery.Dockerfile
    container_name: celery
    restart: always
    command: celery -A app worker --loglevel=INFO
    environment:
      - REDIS_HOST=redis
      - REDIS_PORT=6379
    depends_on:
      - redis
    volumes:
      - ./cv:/app/cv
      - ./jd:/app/jd

  redis:
    image: redis:latest
    restart: always
    container_name: redis
    ports:
      - "6379:6379"

  nginx:
    image: nginx:latest
    restart: always
    container_name: nginx
    ports:
      - "80:80"
    volumes:
      - ./conf:/etc/nginx/conf.d
```