FROM docker.io/node:14-alpine

WORKDIR /usr/src/app

ADD weatherbit/*.patch .

RUN apk add --no-cache --virtual .deps patch  \
  && wget -O - https://github.com/mjesun/loxberry-simple-weather-service/archive/master.tar.gz | tar -xz --strip=2 "loxberry-simple-weather-service-master" \
  && patch service/weatherbit/index.js weatherbit_index_env.patch \
  && apk del .deps \
  && rm -rf weatherbit_index_env.patch \
  && chmod +x ./service/index.js

EXPOSE 6066

ENTRYPOINT [ "node", "./service/index.js" ]
