

FROM node:22.1-alpine3.18 AS builder

WORKDIR /client

COPY ./package*.json ./

RUN npm install 

COPY . .

RUN npm run build

RUN npm prune --production


FROM nginx:alpine

WORKDIR /usr/share/nginx/html

COPY --from=builder /client/build .

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

