Day 29 – Introduction to Docker
Task
Today's goal is to understand what Docker is and run your first container.

You will:

Learn why containers exist and how they differ from VMs
Install Docker on your machine
Run and explore containers from Docker Hub
Expected Output
A markdown file: day-29-docker-basics.md
Screenshots of your running containers
Challenge Tasks
Task 1: What is Docker?
Research and write short notes on:

What is a container and why do we need them?
Containers vs Virtual Machines — what's the real difference?
What is the Docker architecture? (daemon, client, images, containers, registry)
Draw or describe the Docker architecture in your own words.

Task 2: Install Docker
Install Docker on your machine (or use a cloud instance)
Verify the installation
Run the hello-world container
Read the output carefully — it explains what just happened
Task 3: Run Real Containers
Run an Nginx container and access it in your browser
Run an Ubuntu container in interactive mode — explore it like a mini Linux machine
List all running containers
List all containers (including stopped ones)
Stop and remove a container
Task 4: Explore
Run a container in detached mode — what's different?
Give a container a custom name
Map a port from the container to your host
Check logs of a running container
Run a command inside a running container
Hints
docker run, docker ps, docker stop, docker rm
Interactive mode: -it flag
Detached mode: -d flag
Port mapping: -p host:container
Naming: --name
Logs: docker logs
Exec into container: docker exec
Why This Matters for DevOps
Docker is the foundation of modern deployment. Every CI/CD pipeline, Kubernetes cluster, and microservice architecture starts with containers. Today you took the first step.
  answer
