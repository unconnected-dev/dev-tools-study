FROM node

WORKDIR /app

# Moving this line above COPY . /app means we don't RUN npm install layer
# unless needed
COPY package.json /app

RUN npm install

# If code was changed and this line placed before RUN npm install it would
# ignore that layers cache on rebuild
COPY . /app


# This could be removed
# It is optional but recommended / best practice for documentation
EXPOSE 80
# -p is what is required in the command line to export the port
# docker run -p 3000:80


# This would be executed when the image is built
# The image should be the template the container runs off
# RUN node server.js

# This is not executed when image is created but when a container is started 
# based on the image
CMD ["node", "server.js"]

# If a CMD is not specified, the CMD of the base image will be executed
# With no base image and no CMD, you'd get an error