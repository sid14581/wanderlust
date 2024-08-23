#Stage 1
FROM node:22 AS frontend-builder

WORKDIR /frontend-app

COPY package*.json ./

RUN npm install

RUN npm audit fix

COPY . .

#Stage 2
FROM node:22-slim 

WORKDIR /frontend-app

COPY --from=frontend-builder /frontend-app .

COPY .env.sample .env.local

EXPOSE 5173

CMD ["npm","run","dev","--","--host"]
