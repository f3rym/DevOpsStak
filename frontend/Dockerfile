FROM node:20-alpine as builder


ARG REACT_APP_BACKEND_URL
ARG REACT_APP_FRONT_VERSION
ENV REACT_APP_FRONT_VERSION=$REACT_APP_FRONT_VERSION
ENV REACT_APP_BACKEND_URL=$REACT_APP_BACKEND_URL

WORKDIR /app/src

COPY package*.json ./
RUN npm ci --no-audit --maxsockets 1
COPY . .
RUN npm run build

FROM nginx:alpine3.17

COPY --from=builder /app/src/build /var/www/html
COPY --from=builder /app/src/nginx.conf /etc/nginx/nginx.conf 

COPY --from=builder /app/src/entrypoint.sh /entrypoint.sh

RUN chmod +x /entrypoint.sh

ENTRYPOINT [ "/entrypoint.sh" ]

CMD [ "nginx", "-g", "daemon off;" ]