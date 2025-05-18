FROM node
 
WORKDIR /app
 
COPY package.json .
 
RUN npm install
 
COPY . .
 
EXPOSE 80
 
# VOLUME ["logs:/app/logs"]
 
# VOLUME ["/app/node_modules"]

ENV MONGODB_USERNAME=root
ENV MONGODB_PASSWORD=secret

# start is in package.json
CMD ["npm", "start"]