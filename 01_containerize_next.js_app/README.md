## How to Containerize Next.js 14 application

Step 1: Clone This Repository

Step 2: Build a docker image

`docker build -f Dockerfile.dev -t nextjs-app .`

Step 3: Run a docker container with this image

`docker run -p 3000:3000 nextjs-app`