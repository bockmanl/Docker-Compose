# Use an official Node.js runtime as a parent image
FROM node:18-alpine as builder

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code to the working directory
COPY . .

# Building the production application
RUN npm run build

#Server with nginx
FROM nginx:alpine

#Copy files from previous stage to nginx html folder
COPY --from=builder /app/dist /usr/share/nginx/html

# Expose port 80 for the application
EXPOSE 80

#Start nginx server
CMD ["nginx", "-g", "daemon off;"]