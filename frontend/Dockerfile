#----- Stage 1: Build the React application -----
FROM node:22-alpine AS builder

# Set working directory inside the container
WORKDIR /app

# Copy package files and install dependencies
COPY package.json package-lock.json ./
RUN npm install --production=false

# Copy the rest of the application code and build the React app
COPY . .
RUN npm run build


#----- Stage 2: Serve the React application using Nginx -----
FROM nginx:alpine

# Remove the default Nginx static files
RUN rm -rf /usr/share/nginx/html/*

# Copy the built React app from the builder stage to Nginx's html directory
COPY --from=builder /app/build /usr/share/nginx/html

# Copy custom Nginx configuration file
COPY nginx.conf /etc/nginx/conf.d/default.conf


# Expose port 80
EXPOSE 80

# Start Nginx server
CMD ["nginx", "-g", "daemon off;"]