https://www.udemy.com/course/docker-kubernetes-the-practical-guide/
https://labs.play-with-docker.com

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
