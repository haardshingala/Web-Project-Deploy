# 1️⃣ Build stage (runs `npm run build` → `vite build`)
FROM node:18 AS build

WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build          # calls "vite build", outputs /app/dist

# 2️⃣ Serve stage (Nginx serves /app/dist)
FROM nginx:stable-alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
