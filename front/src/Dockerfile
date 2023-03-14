FROM node:18-alpine as build-step
ENV NG_CLI_ANALYTICS=ci
RUN apk update && apk upgrade 
RUN apk add --no-cache bash git cairo pango jpeg giflib python3 pkgconfig build-base g++ cairo-dev jpeg-dev pango-dev giflib-dev
WORKDIR /app
COPY package.json package-lock.json /app
RUN npm install --force
COPY . /app
RUN npm run build --prod

#FROM bunkerity/bunkerized-nginx as prod
FROM nginx as prod
COPY --from=build-step /app/target/classes/static /usr/share/nginx/html
