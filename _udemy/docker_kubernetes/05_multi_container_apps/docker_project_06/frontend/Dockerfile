FROM node

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

# Default port
EXPOSE 3000

# start is in package.json
CMD ["npm", "start"]