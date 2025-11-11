#Building the application
FROM node:24
	
#mkdir /app, cd /app 
WORKDIR /app 

#we are now inside /app

#Copy files from my project into the image. (files can use ".", folders (e.g. public, views) must put name. if not the content will be copied out)
COPY package.json .
COPY package-lock.json .
COPY main.js .
COPY public public 
COPY views views

#Install the dependencies, will create the node_modules
RUN npm ci

#Run the application
ENV APP_PORT=3000
ENV INSTANCE_NAME=""
ENV INSTANCE_HASH=""

#What are the ports the application is listen on
EXPOSE ${APP_PORT}

ENTRYPOINT node main.js 