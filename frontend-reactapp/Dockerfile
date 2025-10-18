FROM node:20-alpine AS build

WORKDIR /react-app

COPY package*.json ./
RUN npm install

COPY . .

# Add permission fix
RUN chmod -R 755 /react-app/node_modules/.bin

# Run build using npx
RUN npx vite build

# Stage 2: serve with nginx
FROM nginx:alpine
COPY --from=build /react-app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
