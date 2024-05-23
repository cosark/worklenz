FROM node:18-alpine

# Install Python, make, and g++ for building native modules
RUN apk add --no-cache python3 make g++

WORKDIR /usr/src/app

# Copy package.json and package-lock.json first to leverage Docker cache
COPY package*.json ./

# Install dependencies globally
RUN npm install -g @angular/cli@latest

# Install project dependencies
RUN npm install

# Copy the rest of the application files
COPY . .

# Expose the necessary port (change according to your app if needed)
EXPOSE 4200

# Start the application
CMD ["npm", "start"]
