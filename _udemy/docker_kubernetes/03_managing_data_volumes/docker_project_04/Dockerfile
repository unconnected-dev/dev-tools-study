FROM node

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 90

# Path in the container, not the host machine
# Creates an anonymous volume
# Named volumes are created in the run command
# VOLUME ["/app/feedback"]

CMD ["node", "server.js"]