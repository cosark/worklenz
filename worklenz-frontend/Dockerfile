# Stage 1: Build the Angular application
FROM node:18-alpine AS builder

# Install Python, make, and g++ for building native modules
RUN apk add --no-cache python3 make g++

WORKDIR /app

# Copy package.json and package-lock.json to leverage Docker cache
COPY package*.json ./

# Install dependencies
RUN npm install -g @angular/cli@latest && npm install

# Copy the application source code
COPY . .

# Build the Angular application
RUN npm run build

# Stage 2: Serve the built application with Nginx
FROM nginx:alpine

# Copy the build output to Nginx's html directory
COPY --from=builder /app/dist/worklenz /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start Nginx server
CMD ["nginx", "-g", "daemon off;"]
