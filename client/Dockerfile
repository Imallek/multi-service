FROM node:16-alpine as builder
WORKDIR /app
COPY package.json .
RUN npm install
COPY . . 
RUN npm build


FROM nginx
EXPOSE 3000
COPY .nginx/default.conf /etc/nginx/conf.d/default.conf
WORKDIR /usr/share/nginx/html
RUN rm -rf ./*
COPY --from=builder /app/build .
ENTRYPOINT [ "nginx", "-g" "daemon off" ]
