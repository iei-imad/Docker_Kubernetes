# Use the official Node image as the base image
FROM node:latest as build

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json to the container
COPY package*.json ./

# Install Angular dependencies
RUN npm install

# Copy the rest of the application code to the container
COPY . .

# Build the Angular application
RUN npm run build --prod

# Use a smaller base image for the final image
FROM nginx:alpine

# Copy the built Angular app to the Nginx HTML directory
COPY --from=build app/dist/angular-16-crud /usr/share/nginx/html

# Expose the port that Nginx will run on
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g","daemon off;"]
