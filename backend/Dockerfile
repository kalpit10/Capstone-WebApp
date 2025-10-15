# ---- Stage 1: Build the Node.js application -----

FROM node:22-alpine AS builder

WORKDIR /app

# Copy package files first for caching
COPY ../package*.json ./

# Install dependencies
RUN npm install

# Copy all backend source files
COPY . .

# ---- Stage 2: Create the final image -----

FROM node:22-alpine 

WORKDIR /app

# Copy everything from the build stage
COPY --from=builder /app /app/

# Expose backend port at 5000
EXPOSE 5000

# Set default env variables
ENV NODE_ENV=development \
    PORT=5000

# Start the Express app
CMD ["npm", "start"]