# Stage 1: build
FROM node:18-alpine AS build
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci
COPY . .
RUN npm run build

# Stage 2: serve with nginx
FROM nginx:1.25-alpine AS runtime
# Copy CRA build output
COPY --from=build /app/build /usr/share/nginx/html
# Copy a default nginx config optimized for SPA routing
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
