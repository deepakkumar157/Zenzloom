# Stage 1: Build the frontend
FROM node:18-alpine AS frontend-build

WORKDIR /app/frontend

# Copy frontend package files and install dependencies
COPY frontend/package.json frontend/package-lock.json ./
RUN npm install --legacy-peer-deps

# Copy frontend source code and build
COPY frontend/ ./
RUN npm run build

# Stage 2: Setup the backend and serve
FROM node:18-alpine

WORKDIR /app

# Copy root package files and install backend dependencies
COPY package.json package-lock.json ./
RUN npm install --production

# Copy backend source code
COPY backend/ ./backend/

# Copy built frontend from Stage 1
COPY --from=frontend-build /app/frontend/dist ./frontend/dist

# Create uploads directory
RUN mkdir -p /app/backend/uploads

# Expose backend port
EXPOSE 5000

# Set environment variables
ENV NODE_ENV=production
ENV PORT=5000

# Start the backend server
CMD ["node", "backend/index.js"]
