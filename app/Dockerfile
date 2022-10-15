FROM node:12-alpine
# Adding build tools to make yarn install work on Apple silicon / arm64 machines
RUN apk add --no-cache python2 g++ make
WORKDIR /app
COPY package.json yarn.lock ./
RUN yarn install --production
COPY . .
CMD ["node", "src/index.js"]

# Maven/Tomcat Example

# FROM maven AS build
# WORKDIR /app
# COPY . .
# RUN mvn package

# FROM tomcat
# COPY --from=build /app/target/file.war /usr/local/tomcat/webapps 

# React Example

# FROM node:12 AS build
# WORKDIR /app
# COPY package* yarn.lock ./
# RUN yarn install
# COPY public ./public
# COPY src ./src
# RUN yarn run build

# FROM nginx:alpine
# COPY --from=build /app/build /usr/share/nginx/html