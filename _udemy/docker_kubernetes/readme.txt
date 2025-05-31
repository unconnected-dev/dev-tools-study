https://www.udemy.com/course/docker-kubernetes-the-practical-guide/
https://labs.play-with-docker.com
https://headsigned.com/posts/mounting-docker-volumes-with-docker-toolbox-for-windows/


docker run --name mongodb -v data:/data/db --rm -d --network my_net -e MONGO_INITDB_ROOT_USERNAME=mongoadmin -e MONGO_INITDB_ROOT_PASSWORD=secret mongo

docker run --name goals-backend --rm -d -p 8080:80 --network my_net -v "/home/paul/_GitHub/dev-tools-study/_udemy/docker_kubernetes/05_multi_container_apps/docker_project_06/backend":/app -v "/home/paul/_GitHub/dev-tools-study/_udemy/docker_kubernetes/05_multi_container_apps/docker_project_06/backend/logs":/app/logs -v /app/node_modules goals-node

docker run --name goals-frontend --rm -p 3000:3000 -d -it -v "/home/paul/_GitHub/dev-tools-study/_udemy/docker_kubernetes/05_multi_container_apps/docker_project_06/frontend/src":/app/src goals-react


Docker
A container technology. A tool for creating and managing containers.


Container
A stardardized unit of software. A package of code and dependencies to run that
code.

The same container always yields the exact same application and behavior. No
matter where or by whom it might be executed.

Support for containers is built into modern operating systems.

Docker simplifies the creation and management of such containers.


Why Containers?
Why would we want independent, stardardized "application packages"?

    Different Development & Production Environments
    We want to have the exact same environment for development and production.
    This ensures that it works exactly as tested
    
    Different Development Environments Within a Team / Company
    It should be easy to share a common development environment / setup with 
    new employees and colleagues

    Clashing Tools / Versions Between Different Projects
    We don't want to uninstall and re-install local dependencies and runtimes
    all the time


Images vs Containers
- Image: A snapshot of a Docker app (code + dependencies)
- Container: A running instance of an image
- You run containers *from* images
- Example: docker run nginx  # runs a container from the nginx image


Image doesn't auto-update
- Editing code locally won't change a built image
- Rebuild image after changes: docker build -t <name> .


Images are read-only
- You can't change an image directly
- Containers add a writable layer on top of the image


Image Tags
- Tag identifies image versions (e.g. nginx:latest, node:18)
- Format: <repository>:<tag>
- Default tag is :latest if not specified
- Tags help manage and pull specific versions


Docker build cache
- Docker uses cached layers to speed up builds
- If one layer changes, all layers after it are rebuilt


Attached vs Detached Mode


Attached vs Detached
- docker run: attached by default (shows output, blocks terminal)
- docker start: detached by default (runs in background)
- Use -d with run for detached: docker run -d nginx
- Use docker attach <name> to connect to running container


Attached Mode:
- Default for `docker run`
- You see the container’s output in your terminal
- Terminal is blocked (you can’t type other commands)
- Exit with Ctrl+C (stops the container unless you handle signals)

Detached Mode (`-d` flag):
- Container runs in background
- Terminal is free for other commands
- No live output shown
- Check output with: docker logs <container>

Example:
- Attached: docker run ubuntu
- Detached: docker run -d nginx


Docker Layers
- Images are built in layers, one per Dockerfile instruction
- Layers are cached and reused to speed up builds
- Changing one layer causes all layers after it to rebuild
- Use `docker history <image>` to see layer info


Docker volumes are used to persist data outside of containers. They let you:

    Keep data between container restarts

    Share data between containers

By default, Docker stores volumes in /var/lib/docker/volumes/.

Volumes are folders on your host machine hard drive which are mounted 
("made available", mapped) into containers.

Volumes persist if a container shuts down. If a container restarts and mounts
a volume, any data inside of that volume is available in the container.


Anonymous Volumes
- Created when using VOLUME in Dockerfile or -v without a name
- Docker assigns a random name
- Not easy to reuse or manage manually
- Persist data, but can pile up if not cleaned
- View with: docker volume ls


Named Volumes
- Explicitly created and easy to manage
- Format: -v <volume_name>:<container_path>
- Data persists across container restarts/removals
- Create with docker volume create <name>
- View with docker volume ls


Volumes on container removal
- Anonymous volumes: deleted when container is removed (unless --volumes flag is omitted)
- Named volumes: persist even after container removal
- Use --volumes (-v) with docker rm to remove volumes too
- Safer to use named volumes for persistent data


Why volumes remain after container removal:
- Named volumes persist until explicitly deleted
- Anonymous volumes tied to containers get removed only if you use `docker rm -v`
- Some volumes may be in use by other containers
- Volumes created manually or by Docker Compose remain until pruned

Tip:
- Use `docker volume prune` to remove all unused volumes safely
- Check which containers use a volume: `docker ps -a --filter volume=<volume_name>`



Docker sets up a folder / path on your host machine, the exact location is unknown
to you (dev). Managed via docker volume commands.

A defined path in the container is mapped to the created volume/mount.


docker run -p 3000:80 -d -v feedback:/app/feedback --name feedback-app feedback-node:volumes
- Runs container in detached mode
- Maps host port 3000 → container port 80
- Uses named volume "feedback" at /app/feedback (persists data)
- Names the container "feedback-app"
- Uses image "feedback-node:volumes"


Bind Mounts
- Link a host directory directly into the container
- Format: -v /host/path:/container/path
- Reflects live changes (great for dev)
- Example: docker run -v $(pwd):/app my-image
- Path must exist on host (unlike named volumes)


Volume/Bind Mount Path Priority
- If multiple mounts target the same path, **the last one wins**
- In your command:
  - feedback:/app/feedback mounts first
  - then the bind mount to /app overrides everything under /app (including /app/feedback)
- So, /app/feedback from the container image or named volume is hidden by the host’s /app

Tip:
- Avoid overlapping mount paths to prevent unexpected hiding
- Separate data and code paths cleanly (e.g., mount code to /app and data to /data)


docker run -v /app/data ...                     Anonymous Volume
docker run -v data:/app/data ...                Named Volume
docker run -v /path/to/code:/app/code ...       Bind Mount


Anonymous Volumes
Created specifically for a single container
Survives container shurtdown / restart unless --rm is used
Can not be shared across containers
Since it's Anonymous, it can't be reused (even on same images)


Named Volumes
Created in general - not tied to any specific container
Survives container shutdown / restart - removal via Docker CLI
Can be shared across containers
Can be re-used for same container (across restarts)

Binds Mounts
Location on host file system, not tied to any specific container
Survives container shutdown / restart - removal on host fs
Can be shared across containers
Can be re-used for same container (across restarts)



Read-Only Volumes
- Mounts can be made read-only using :ro
- Seems to be good practice to avoid unintentional bugs
- Prevents container from modifying the content
- Format: -v <source>:<target>:ro
- Example: docker run -v /data:/app/data:ro my-image



Arguments vs Environment Variables

Build-time: ARG
- Defined in Dockerfile with ARG
- Set during build: docker build --build-arg NAME=value
- Not persisted in final image
- Not accessible in CMD or any application code

Run-time: ENV
- Set in Dockerfile (ENV) or at run: docker run -e NAME=value
- Default in Dockerfile but it can be overwritten in run command
- Available inside container at runtime
- Used for config, secrets, ports, etc.
- Availabe inside of Dockerfile and in application code


Docker Networks
- Allow containers to communicate with each other
- Types:
  • bridge (default): isolated, local container network
  • host: uses host’s network stack (Linux only)
  • none: no network
- Create custom bridge: docker network create my-net
- Connect with: docker run --network my-net ...
- Containers on same user-defined bridge can resolve each other by name

Within a Docker network, all containers can communicate with each other and IPs
are automatically resolved
Docker does not automatically create networks, they need to be created via command

If two Docker containers are part of the same network you can put the container name
in directly as a domain and Docker will translate the name to the IP address of the 
container



How Docker Resolves IP Addresses

- Containers on the same user-defined bridge network can resolve each other by **name**
- Docker uses an internal DNS server to map container names to IPs
- Example: ping another container using its name: `ping my-db`
- IPs are dynamically assigned; use container names, not IPs, for reliability
- Use `docker network inspect <network>` to see name-IP mappings


Docker Network Drivers

1. bridge (default)
- Local, isolated network on the Docker host
- Containers can communicate by name if on same user-defined bridge

2. host
- Shares host's network stack (no isolation)
- No port mapping needed; container uses host's ports directly

3. overlay
- Enables multi-host container communication
- Used with Docker Swarm
- Requires key-value store or Swarm manager

4. macvlan
- Assigns MAC address from host's network to container
- Container behaves like a physical device on the LAN
- Advanced use, often needs manual host config

5. none
- Disables all networking (no external access)

6. third-party plugins
- Extend Docker networking (e.g., Weave, Calico, Cilium)
- Add features like encryption, policy control, cross-data center support


Docker Compose
- Tool for defining and running multi-container Docker apps
- Uses a YAML file (docker-compose.yml) to configure services, networks, and volumes
- Key command: docker compose up
  • Builds, (re)creates, and starts containers
- Key benefits:
  • Easier multi-container setup
  • Versioned config in code
  • Shared networks by default
