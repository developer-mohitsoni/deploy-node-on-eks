FROM node:18-alpine AS builder

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

RUN npm run build

FROM nginx:stable-alpine

RUN mkdir /usr/share/nginx/buffer

COPY --from=builder /app/out /usr/share/nginx/html
COPY --from=builder /app/public /usr/share/nginx/html
ARG env=prod
COPY conf/$env/nginx.conf /etc/nginx/conf.d/default.conf

RUN mkdir /usr/share/nginx/log

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
