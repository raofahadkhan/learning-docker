# Containerization of Fast Api Application

This repository demonstrates how to containerize a Next.js 14 application using Docker.

## Prerequisites

- Python (version >= 3.12)
- Docker

## Steps to Containerize

1. **Create a Next.js 14 Application**

   ```bash
   poetry new demo_app
   cd demo_app
   poetry add fastapi uvicorn
   ```

2. **Create a main.py file and add the below code into it**

   ```bash
    from fastapi import FastAPI

    app = FastAPI()

    @app.get("/")
    async def root():
    return {"message": "Hello World"}
   ```

2. **Run the Application Locally**

```bash
poetry run uvicorn demo_app.main:app --host 0.0.0.0 --reload
```

3. **Create Dockerfile**

Create a file named `Dockerfile.dev` in the root of your project with the following content:

```dockerfile
FROM python:3.12

LABEL maintainer="raofahad046@gmail.com"

WORKDIR /code

RUN apt-get update && apt-get install -y \
    build-essential \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*

RUN pip install poetry

COPY . /code/

RUN poetry config virtualenvs.create false

RUN poetry install

EXPOSE 8000

CMD [ "poetry", "run", "uvicorn", "demo_app.main:app", "--host", "0.0.0.0", "--reload" ]
```

4. **Build Docker Image**

Build the Docker image using the following command:

```bash
docker build -f Dockerfile.dev -t contName:latest .
```
5. **Run the Docker Container**

Run the container using the following command:

```bash
docker run -d -p 8000:8000 --name fastapiCont1 contName:latest
```


### Additional Information

```markdown
## Additional Information

- The `Dockerfile.dev` is set up to use Python and Poetry to manage dependencies.
- The application is exposed on port 8000.
- The container is started with the `uvicorn` server for a FastAPI application (`demo_app.main:app`). Adjust the `CMD` line in `Dockerfile.dev` to match your actual application's entry point.

Feel free to contribute or raise issues for any problems you encounter. Happy coding!

