FROM node:15 as builder

WORKDIR /app

COPY package.json package-lock.json ./

RUN npm ci

COPY . .

RUN npm run build

FROM nginx:1.19-alpine

COPY --from=builder /app/build /usr/share/nginx/html

RUN sed -i 's/listen       80;/listen 8080;/g' /etc/nginx/conf.d/default.conf

EXPOSE 8080 

CMD ["nginx", "-g", "daemon off;"]