# # dev environment
# FROM node:16-alpine

# WORKDIR /app/frontend/

# COPY package*.json /app/frontend/
# RUN npm install

# COPY . /app/frontend/

# # Dev
# CMD ["npm", "run", "start-watch"]



# build environment
FROM node:16-alpine as build
WORKDIR /app/frontend/
COPY package*.json /app/frontend/
RUN npm install
COPY . /app/frontend/
RUN npm run build

# production environment
FROM nginx:stable-alpine
COPY --from=build /app/frontend/build /usr/share/nginx/html
COPY --from=build /app/frontend/nginx/default.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

