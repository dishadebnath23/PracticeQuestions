Practice Questions – Day 14  
Docker

------------------------------------------------------------

1. Explain how you dockerised your application end-to-end.

I dockerised my application by:
- Creating a Dockerfile for the backend application
- Building a Docker image from the Dockerfile
- Running the image as a container
- Using Docker Compose to manage multiple services

End-to-end flow:
1. Write Dockerfile
2. Build image using docker build
3. Run container using docker run
4. Connect services using Docker Compose

------------------------------------------------------------

Follow-up: What base image did you choose and why?

I chose a lightweight base image like:
- openjdk for Spring Boot
- node for frontend (if required)

Reason:
- Smaller image size
- Faster build and startup
- Official and stable images

------------------------------------------------------------

Follow-up: How do you expose ports?

Ports are exposed using:
- EXPOSE instruction in Dockerfile
- Port mapping using -p flag or Docker Compose

This allows external traffic to access the container.

------------------------------------------------------------

Follow-up: How do you pass environment variables?

Environment variables are passed using:
- ENV instruction in Dockerfile
- environment section in docker-compose.yml
- --env flag while running container

============================================================

2. What is the difference between a Docker image and a Docker container?

Docker Image:
- Blueprint of the application
- Read-only
- Built using Dockerfile

Docker Container:
- Running instance of an image
- Has writable layer
- Executes the application

------------------------------------------------------------

Follow-up: Can multiple containers run from the same image?

Yes.

Multiple containers can be created from the same image,  
each running independently.

------------------------------------------------------------

Follow-up: What happens when a container stops?

When a container stops:
- Application execution ends
- Container state is preserved
- Data inside container is lost unless volumes are used

============================================================

3. What is a Dockerfile?  
Explain the important instructions you used.

Dockerfile:
- A text file with instructions to build an image

Important instructions:
- FROM → defines base image
- WORKDIR → sets working directory
- COPY → copies files into image
- RUN → executes commands
- EXPOSE → documents port
- CMD / ENTRYPOINT → starts application

------------------------------------------------------------

Follow-up: Difference between CMD and ENTRYPOINT

CMD:
- Provides default command
- Can be overridden

ENTRYPOINT:
- Defines fixed executable
- CMD acts as arguments

------------------------------------------------------------

Follow-up: Purpose of EXPOSE

EXPOSE:
- Documents the port used by container
- Does not publish port by itself
- Helps in container communication

------------------------------------------------------------

Follow-up: Why layer ordering matters?

Layer ordering matters because:
- Docker caches layers
- Proper ordering improves build speed
- Reduces unnecessary rebuilds

============================================================

4. Why do we use Docker Compose?  
How did you use it in your project?

Docker Compose is used to:
- Run multiple containers together
- Manage services using single file
- Simplify environment setup

In my project, I used it to:
- Run backend service
- Connect database
- Connect Kafka (if used)

------------------------------------------------------------

Follow-up: How did you connect backend, database, and Kafka?

They were connected using:
- Same Docker network
- Service names as hostnames
- Docker Compose service definitions

------------------------------------------------------------

Follow-up: What is the role of depends_on?

depends_on:
- Controls startup order
- Ensures dependent services start first
- Does not wait for service readiness

------------------------------------------------------------

Follow-up: How do services communicate in Docker Compose?

Services communicate using:
- Service names as DNS hostnames
- Internal Docker network
- Exposed ports (if needed)

============================================================

5. How do you handle configuration and secrets in Docker?

Configuration and secrets are handled using:
- Environment variables
- External configuration files
- Docker secrets (in production)

------------------------------------------------------------

Follow-up: Environment variables vs properties file

Environment variables:
- Dynamic
- Environment-specific
- Preferred for Docker

Properties file:
- Static
- Less flexible
- Not ideal for containers

------------------------------------------------------------

Follow-up: How are DB credentials passed?

DB credentials are passed using:
- Environment variables
- Docker Compose environment section
- External secret managers

------------------------------------------------------------

Follow-up: Why should secrets not be hardcoded in images?

Secrets should not be hardcoded because:
- Images are shared
- Security risk
- Hard to rotate credentials

------------------------------------------------------------
