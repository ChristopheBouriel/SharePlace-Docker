FROM node:12.7-alpine

RUN mkdir -p /app
WORKDIR /app

COPY package.json /app

COPY . /app

RUN npm install

RUN apk update && apk add bash

CMD ["npm", "start"]