# Build stage
FROM node:16-alpine AS build

# Install zip utility
RUN apk add --no-cache zip

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
COPY package*.json ./
RUN npm ci

# Bundle app source
COPY . .

# Build the application
RUN npm run build

# Production stage
FROM node:16-alpine

# Create app directory
WORKDIR /usr/src/app

# Copy only the necessary files from the build stage
COPY --from=build /usr/src/app/www ./www

# Install only production dependencies
COPY package*.json ./
RUN npm ci --only=production && npm cache clean --force

# Expose the port
EXPOSE 8080

# Run the application
CMD [ "node", "./www/server.js" ]
