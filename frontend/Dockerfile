# Base image
FROM node:20-alpine

# Create app directory
WORKDIR /frontend

# A wildcard is used to ensure both package.json AND package-lock.json are copied
COPY package.json .

# Install app dependencies
RUN npm i

# Bundle app source
COPY . .

EXPOSE 3000

COPY . .

# Start the server using the production build
CMD [ "node", "server.js" ]