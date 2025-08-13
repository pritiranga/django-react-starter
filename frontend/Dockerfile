# Stage 1: Build React app
FROM node:18 AS build

# Set working directory inside container
WORKDIR /app

# Copy package.json and package-lock.json from root
COPY package*.json ./

# Install dependencies
RUN npm install --silent

# Copy everything from root
COPY . .

# Build React app (inside frontend folder)
WORKDIR /app/frontend
RUN npm run build

# Stage 2: Serve using Nginx
FROM nginx:1.25-alpine

# Copy build files from previous stage
COPY --from=build /app/frontend/build /usr/share/nginx/html

# Expose port 80 for Nginx
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
