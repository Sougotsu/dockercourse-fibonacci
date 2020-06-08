# Use an existing docker image as a base
FROM node:alpine

# Setting working directory
WORKDIR /app

# Copy package json to image/container before rest of files
# to avoid unnecesary rebuilds
COPY package*.json ./

# Download an install a dependency
RUN npm install

# Copy files to image/container
COPY ./ ./

RUN npm run build

FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=0 /app/build /usr/share/nginx/html