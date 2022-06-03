FROM node:12-alpine3.14

WORKDIR /app

#We will use this directory to store files, run npm, and launch our application 

COPY package.json /app

#RUN npm ci --only=production (for production build when we have ci|cd)

COPY . /app

CMD node index.js

EXPOSE 8081
