FROM node:18-alpine AS builder
RUN apk add --no-cache python3 make g++

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install --only=production

FROM node:18-alpine

WORKDIR /usr/src/app

COPY --from=builder /usr/src/app/node_modules ./node_modules
COPY . .

EXPOSE 7000

ENTRYPOINT ["node", "server.js"]