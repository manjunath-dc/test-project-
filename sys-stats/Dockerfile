FROM node:10

RUN mkdir -p /opt/app

# Add source files & deps
WORKDIR /opt/app

COPY . /opt/app
RUN rm -rf node_modules/* 
#RUN env:NODE_OPTIONS = "--openssl-legacy-provider"
RUN npm install

EXPOSE 3000

ENTRYPOINT npm start

