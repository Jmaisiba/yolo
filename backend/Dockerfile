
FROM node:22.1-alpine3.18

WORKDIR /backend

COPY ./package*.json ./

RUN npm install 

COPY . .


CMD ["npm" , "start"]


EXPOSE 5000	
