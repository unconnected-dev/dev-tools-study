FROM node:14

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 80

# Path in the container, not the host machine
# Creates an anonymous volume
# Named volumes are created in the run command
# VOLUME ["/app/feedback"]

# This could be used instead of putting an anonymous volume
# in the run command -v /app/node_modules
# VOLUME ["/app/node_modules"]


# CMD ["node", "server.js"]
CMD ["npm", "start"]