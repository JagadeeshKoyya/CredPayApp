#stage:build
FROM node:22-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci

#Copy the rest of the application code to the working directory
COPY . .
RUN npm run build

#stage:serve the dist to nginx
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

#Expose port 80 to the outside world
EXPOSE 80