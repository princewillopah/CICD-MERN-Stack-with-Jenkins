# # Use the official Node.js image as the base image for building the frontend
# FROM node:16-alpine AS build

# # Set the working directory
# WORKDIR /app

# # Copy package.json and package-lock.json
# COPY package*.json ./

# # Install dependencies
# RUN npm install

# # Copy the rest of the application code
# COPY . .

# # Build the React application
# RUN npm run build

# # Use the official Nginx image to serve the frontend
# FROM nginx:alpine

# # Copy the build output to Nginx's html directory
# COPY --from=build /app/build /usr/share/nginx/html

# # go to the root folder(../) and enter nginx folder(..//nginx) and Copy custom the
# # Nginx configuration(../nginx/nginx.conf ) to the 
# # nginx container file system directory (/etc/nginx/nginx.conf)
# COPY nginx.conf /etc/nginx/nginx.conf


# COPY default.conf /etc/nginx/conf.d/default.conf

# # Expose port 80
# EXPOSE 80

# # Command to start Nginx
# CMD ["nginx", "-g", "daemon off;"]

# ========================================
#  using serve
# ========================================


# Use the official Node.js image as the base image
FROM node:16-alpine AS build

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the React application
RUN npm run build

# Use a lightweight web server to serve the build directory
FROM node:16-alpine

# Install serve to serve the build directory
RUN npm install -g serve

# Set the working directory
WORKDIR /app

# Copy the build output from the previous stage
COPY --from=build /app/build ./build

# Expose port 3000 (or any port you want your app to run on)
EXPOSE 3000

# Command to serve the app
CMD ["serve", "-s", "build", "-l", "3000"]