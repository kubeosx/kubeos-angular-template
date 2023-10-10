# Use the official Node.js image as a parent image for building the Angular app
FROM node:18 as build

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install application dependencies
RUN npm install

# Copy the rest of the application code to the working directory
COPY . .

# Build the Angular app (adjust the command as needed based on your app's configuration)
RUN npm run build

# Use the official Nginx image as a parent image for serving the built Angular app
FROM nginx:latest

# Set the working directory inside the container
WORKDIR /usr/share/nginx/html

# Remove the default Nginx welcome page
RUN rm -f index.html

# Copy the built Angular app from the build stage into the Nginx image
COPY --from=build /app/dist/ .

# Expose port 80 for incoming traffic
EXPOSE 80
