FROM node:18

# Create app directory
WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy certificates directory first
COPY certs/ ./certs/

# Copy source code (excluding what's in .dockerignore)
COPY . .

# Expose HTTPS port
EXPOSE 8443

# Start the server
CMD ["npm", "run", "start:env"]