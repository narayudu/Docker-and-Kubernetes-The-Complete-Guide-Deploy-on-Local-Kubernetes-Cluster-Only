FROM node:alpine as builder

# RUN apk update && apk upgrade && \
#  apk add --no-cache vim bash git curl

WORKDIR /app
COPY ./package.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx 

RUN apt-get update && apt-get upgrade && \
    apt-get install -y vim bash git curl

EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/build /usr/share/nginx/html
