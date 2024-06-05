
FROM node:13.12-alpine

WORKDIR /backend

COPY ./package*.json ./

RUN npm install 

COPY . .


CMD ["npm" , "start"]


EXPOSE 5000	
