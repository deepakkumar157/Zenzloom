# Base image
FROM node:18

# Working directory
WORKDIR /app

# Copy package files first
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy remaining project files
COPY . .

# Expose port (MERN backend usually 5000)
EXPOSE 5000

# Start app
CMD ["npm", "start"]
