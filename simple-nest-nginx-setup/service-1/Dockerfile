# Base image
FROM node:18-alpine

# Set working directory
WORKDIR /app

# Copy project files
COPY . .

# Install dependencies
RUN npm install

# Build the app
RUN npm run build

# Expose the port the app runs on
EXPOSE 3001

# Start the app
CMD ["npm", "run", "start:prod"]