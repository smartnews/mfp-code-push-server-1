FROM node:18-alpine

# Install system dependencies and networking tools
RUN apk add --no-cache python3 make g++ netcat-openbsd curl iputils

# Create app directory
WORKDIR /app

# Copy package files
COPY package*.json ./

# Copy certificates directory first
COPY certs/ ./certs/

# Copy source code (excluding what's in .dockerignore)
COPY . .

# Ensure correct permissions for certificates
RUN chmod 600 ./certs/*

# Add healthcheck for Redis connectivity
HEALTHCHECK --interval=30s --timeout=10s --start-period=5s --retries=3 \
    CMD redis-cli -h redis ping || exit 1

# Expose HTTPS port
EXPOSE 8443

# Start the server
CMD ["npm", "run", "start:env"]