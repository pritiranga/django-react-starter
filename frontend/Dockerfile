
# frontend/Dockerfile

# Stage 1: Build the React app
FROM node:18 AS build

# Set working directory inside container
WORKDIR /app

# Copy package.json and package-lock.json first (to leverage caching)
COPY package*.json ./

# Install dependencies
RUN npm install --silent

# Copy the rest of the app source code
COPY . .

# Build the app for production
RUN npm run build

# Stage 2: Serve the app using a lightweight web server
FROM nginx:1.25-alpine

# Copy build output from previous stage to Nginx HTML folder
COPY --from=build /app/build /usr/share/nginx/html

# Copy custom Nginx config (optional, if you need rewrites for React Router)
# COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 80 for the container
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
