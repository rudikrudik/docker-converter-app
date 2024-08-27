FROM node:13 AS node
WORKDIR /app/apps/app
COPY ./apps/app/*.json ./
RUN npm ci
COPY . ../../
WORKDIR /app
RUN npm i
WORKDIR /app/apps/app
ARG env=prod
RUN PUBLIC_URL=http://localhost:3001 npm run build

FROM nginx:1.13
COPY --from=node /app/apps/app/build /usr/share/nginx/html
COPY ./apps/app/nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
