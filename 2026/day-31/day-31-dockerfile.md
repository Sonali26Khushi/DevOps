Day 31 – Dockerfile & Custom Images
Task 1: Your First Dockerfile
Create Project Folder
mkdir my-first-image
cd my-first-image
Create Dockerfile

Create a file named:

Dockerfile

Add this content:

FROM ubuntu

RUN apt update && apt install curl -y

CMD ["echo", "Hello from my custom image!"]
What Each Line Does
Instruction	Purpose
FROM ubuntu	Uses Ubuntu as base image
RUN	Executes commands during image build
CMD	Default command when container starts
Build the Image
docker build -t my-ubuntu:v1 .

Explanation:

-t → tag image
. → current directory is build context
Verify Image
docker images

You should see:

my-ubuntu   v1
Run the Container
docker run my-ubuntu:v1

Expected output:

Hello from my custom image!
Task 2: Dockerfile Instructions
Create Another Project
mkdir dockerfile-demo
cd dockerfile-demo
Create app.py
print("Dockerfile Instructions Demo")
Create Dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY app.py .

RUN pip install flask

EXPOSE 5000

CMD ["python", "app.py"]
Explanation of Instructions
Instruction	Meaning
FROM	Base image
WORKDIR	Sets working directory
COPY	Copies files into image
RUN	Executes build commands
EXPOSE	Documents container port
CMD	Default startup command
Build the Image
docker build -t python-demo:v1 .
Run the Container
docker run python-demo:v1

Expected output:

Dockerfile Instructions Demo
Task 3: CMD vs ENTRYPOINT
Example 1: CMD
Dockerfile
FROM alpine

CMD ["echo", "hello"]

Build:

docker build -t cmd-demo .

Run:

docker run cmd-demo

Output:

hello
Override CMD
docker run cmd-demo ls

Result:

Default CMD gets replaced
ls command runs instead
Example 2: ENTRYPOINT
Dockerfile
FROM alpine

ENTRYPOINT ["echo"]

Build:

docker build -t entry-demo .

Run:

docker run entry-demo hello world

Output:

hello world
Difference Between CMD and ENTRYPOINT
CMD	ENTRYPOINT
Can be overridden easily	Fixed main command
Default arguments	Main executable
Flexible	Strict behavior
When to Use CMD vs ENTRYPOINT
Use CMD When:
You want flexible commands
Users may override behavior

Example:

Ubuntu shell
Development containers
Use ENTRYPOINT When:
Container should always run a specific executable

Example:

Nginx
Database containers
Application containers
Task 4: Build a Simple Web App Image
Create Project Folder
mkdir my-website
cd my-website
Create index.html
<!DOCTYPE html>
<html>
<head>
  <title>My Docker Website</title>
</head>
<body>
  <h1>Hello from Docker Nginx!</h1>
</body>
</html>
Create Dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/

EXPOSE 80
Build Image
docker build -t my-website:v1 .
Run Container
docker run -d -p 8080:80 --name mysite my-website:v1
Access in Browser
http://localhost:8080

You should see your custom webpage.

Task 5: .dockerignore
Create .dockerignore File
node_modules
.git
*.md
.env
Why Use .dockerignore?

It prevents unnecessary files from being copied into the image.

Benefits:

Faster builds
Smaller image size
Better security
Cleaner images
Verify Ignored Files

Build image again:

docker build -t ignore-demo .

Ignored files will not be included in build context.

Task 6: Build Optimization
Example Dockerfile
FROM node:20

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

CMD ["npm", "start"]



Why This Order Matters

Docker caches layers.

If application code changes:

COPY . . layer rebuilds
npm install layer stays cached

This makes builds much faster.

Bad Dockerfile Order
COPY . .

RUN npm install

Problem:

Any code change invalidates cache
Dependencies reinstall every build
Why Layer Order Matters
Best Practice

Place:

Stable layers first
Frequently changing layers last

Benefits:

Faster CI/CD pipelines
Reduced build time
Better developer productivity
Important Dockerfile Commands Summary
Command	Purpose
FROM	Base image
RUN	Execute commands during build
COPY	Copy files into image
WORKDIR	Set working directory
EXPOSE	Document ports
CMD	Default startup command
ENTRYPOINT	Fixed executable
.dockerignore	Exclude unnecessary files
Important Docker Build Commands
Command	Purpose
docker build -t name .	Build image
docker run image	Run container
docker images	List images
docker ps	List running containers
docker logs	View logs
Key Learning Summary
Relationship Between Dockerfile and Image
Dockerfile → Docker Image → Docker Container
Dockerfile defines instructions
Docker builds image from Dockerfile
Containers run from images
