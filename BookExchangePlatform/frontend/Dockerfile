# 1️⃣ Build stage
FROM node:18-alpine AS build

WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build          # typically runs `vite build` → outputs to /app/dist

# 2️⃣ Serve stage (Node.js with 'serve' to serve /dist)
FROM node:18-alpine

WORKDIR /app

# Install serve (lightweight static file server)
RUN npm install -g serve

# Copy build output from the previous stage
COPY --from=build /app/dist ./dist

# Use a non-root user for security
RUN adduser -D appuser
USER appuser

# Expose default serve port
EXPOSE 3000

# Start the static file server
CMD ["serve", "-s", "dist", "-l", "3000"]
