### Build
FROM node:16 AS ionic
## Create app directory
WORKDIR /usr/src/app
## Install app dependencies
RUN npm install -g ionic
## A wildcard is used to ensure both package.json AND package-lock.json are copied
COPY package*.json ./
RUN npm install -f
## Bundle app source
COPY . .
# Run ionic build without NODE_OPTIONS
RUN ionic build
### Run 
FROM nginx:alpine
COPY --from=ionic /usr/src/app/www /usr/share/nginx/html