FROM node:10.23.0
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 6969
CMD [ "node", "server.js" ]
