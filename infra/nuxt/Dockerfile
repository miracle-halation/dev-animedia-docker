FROM node:16-alpine3.14

WORKDIR /frontend

ADD package.json /frontend/package.json

ADD . /frontend

RUN yarn install
RUN yarn build

EXPOSE 3000

CMD ["yarn", "start"]