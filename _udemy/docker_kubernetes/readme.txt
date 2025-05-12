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
