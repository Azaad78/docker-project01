# Filename: Dockerfile
FROM node:10-alpine as Yarn

RUN mkdir -p /app/bgshop
WORKDIR /app/bgshop
ENTRYPOINT ["yarn"]

COPY package.json ./
RUN yarn
COPY . .

ARG REACT_APP_BASE_URL="http://localhost:2370"
ENV REACT_APP_BASE_URL="${REACT_APP_BASE_URL}"

RUN yarn build

FROM nginx:stable-alpine as Web

COPY docker/nginx /etc/nginx
RUN rm -rf /usr/share/nginx/html/*
COPY --from=Yarn /app/bgshop/build /usr/share/nginx/html

#CMD tail -f /dev/null