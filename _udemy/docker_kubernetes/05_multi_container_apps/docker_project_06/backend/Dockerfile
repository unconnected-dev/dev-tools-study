FROM node
 
WORKDIR /app
 
COPY package.json .
 
RUN npm install
 
COPY . .
 
EXPOSE 80
 
# VOLUME ["logs:/app/logs"]
 
# VOLUME ["/app/node_modules"]

ENV MONGODB_USERNAME=mongoadmin
ENV MONGODB_PASSWORD=secret

# start is in package.json
# nodemon watches the project folder for changes in javascript files 
# and will restart the node server if they occur
# it can be verified by checking the container logs
# docker logs <container-name>
CMD ["npm", "start"]