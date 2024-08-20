FROM node:22

WORKDIR /backend-app

COPY . .

RUN npm i

COPY .env.sample .env

EXPOSE 5000

CMD ["npm","start"]

