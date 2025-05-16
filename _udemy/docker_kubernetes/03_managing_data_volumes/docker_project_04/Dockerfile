FROM node:14

WORKDIR /app

COPY package.json .

RUN npm install

# This could be commented out as we bind mount the entire directory
# But this is only due to the command we use being specific for development
# which allows changes to the code to be reflected without rebuilding
# the image
COPY . .

# ARG and ENV insturctions add layers to the docker file
# If they change all subsequent layers are rebuilt, so best to be aware
ARG DEFAULT_PORT=80

ENV PORT=$DEFAULT_PORT

# EXPOSE 80
# Will get the port ENV set prior
EXPOSE $PORT

# Path in the container, not the host machine
# Creates an anonymous volume
# Named volumes are created in the run command
# VOLUME ["/app/feedback"]

# This could be used instead of putting an anonymous volume
# in the run command -v /app/node_modules
# VOLUME ["/app/node_modules"]

# Can only override readonly via run in the command line
# VOLUME ["/app/temp"]
# docker run 
    # -p 3000:80 -d 
    # --name feedback-app 
    # -v feedback:/app/feedback 
    # -v "/home/paul/_GitHub/dev-tools-study/_udemy/docker_kubernetes/03_managing_data_volumes/docker_project_04:/app:ro" 
    # -v /app/temp 
    # -v /app/node_modules 
    # feedback-node:volumes

# CMD ["node", "server.js"]
CMD ["npm", "start"]