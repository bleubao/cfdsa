#Building the application
FROM node:24 AS build
	
#mkdir /app, cd /app 
WORKDIR /src 

#we are now inside /app

RUN npm install -g @angular/cli

#Copy files from my project into the image. (files can use ".", folders (e.g. public, views) must put name. if not the content will be copied out)
COPY *.json .
COPY public public 
COPY src src

#Install the dependencies, will create the node_modules

RUN npm ci && ng build

FROM caddy:2.10

# Create HTML directory to serve from
WORKDIR /app

COPY caddy/Caddyfile .

RUN mkdir html
COPY caddy/error.html html
COPY --from=build /src/dist/angular/browser/ html

ENV CADDY_PORT=3000

EXPOSE ${CADDY_PORT}

# Use Caddy as entrypoint (default in the base image)
ENTRYPOINT caddy run --config=/app/Caddyfile