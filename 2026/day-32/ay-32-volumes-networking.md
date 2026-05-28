Day 32 – Docker Volumes & Networking
Task
Today's goal is to solve two real problems: data persistence and container communication.

Containers are ephemeral — they lose data when removed. And by default, containers can't easily talk to each other. Today you fix both.

Expected Output
A markdown file: day-32-volumes-networking.md
Screenshots of your experiments
Challenge Tasks
Task 1: The Problem
Run a Postgres or MySQL container
Create some data inside it (a table, a few rows — anything)
Stop and remove the container
Run a new one — is your data still there?
Write what happened and why.

Task 2: Named Volumes
Create a named volume
Run the same database container, but this time attach the volume to it
Add some data, stop and remove the container
Run a brand new container with the same volume
Is the data still there?
Verify: docker volume ls, docker volume inspect

Task 3: Bind Mounts
Create a folder on your host machine with an index.html file
Run an Nginx container and bind mount your folder to the Nginx web directory
Access the page in your browser
Edit the index.html on your host — refresh the browser
Write in your notes: What is the difference between a named volume and a bind mount?

Task 4: Docker Networking Basics
List all Docker networks on your machine
Inspect the default bridge network
Run two containers on the default bridge — can they ping each other by name?
Run two containers on the default bridge — can they ping each other by IP?
Task 5: Custom Networks
Create a custom bridge network called my-app-net
Run two containers on my-app-net
Can they ping each other by name now?
Write in your notes: Why does custom networking allow name-based communication but the default bridge doesn't?
Task 6: Put It Together
Create a custom network
Run a database container (MySQL/Postgres) on that network with a volume for data
Run an app container (use any image) on the same network
Verify the app container can reach the database by container name
Hints
Volumes: docker volume create, -v volume_name:/path
Bind mount: -v /host/path:/container/path
Networking: docker network create, --network
Ping: docker exec container1 ping container2
Submission
