
FROM node:22.1-alpine3.18

WORKDIR /backend

COPY ./package*.json ./

RUN npm install

COPY . .

EXPOSE 5000

CMD npm start

	