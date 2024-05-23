# Use the official Node.js image as the base image for building
FROM node:16-alpine AS build

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# You can include a build step here if necessary, e.g., transpiling code
# RUN npm run build

# Create a minimal final image
FROM node:16-alpine

WORKDIR /app

# Copy only necessary files from the build stage
COPY --from=build /app .

# Create and use a non-root user
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser

# Expose the port the app runs on
EXPOSE 5000

# Command to run the application
CMD ["node", "server.js"]

