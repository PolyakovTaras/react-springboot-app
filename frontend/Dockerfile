FROM node:12-alpine as builder

WORKDIR /app

COPY package.json /app/package.json

RUN npm install --only=prod

COPY . /app

RUN npm run build


FROM nginx:1.16.0-alpine

RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d/

COPY --from=builder /app/build /usr/share/nginx/html

EXPOSE 3000

CMD ["nginx", "-g", "daemon off;"]
