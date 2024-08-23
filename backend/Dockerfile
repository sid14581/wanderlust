
#Stage 1
FROM node:22 AS backend_builder

WORKDIR /backend-app

COPY . .

RUN npm i

RUN npm run test

#Stage 2
FROM node:22-slim

WORKDIR /backend-app

COPY --from=backend_builder /backend-app .

COPY .env.sample .env

EXPOSE 5000

CMD ["npm","start"]

