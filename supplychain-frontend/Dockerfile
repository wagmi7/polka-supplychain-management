FROM node:18-alpine

WORKDIR /supplychain-frontend

COPY /supplychain-frontend/package.json .
COPY /supplychain-frontend/yarn.lock .
COPY /supplychain-frontend/.yarnrc.yml .
COPY /supplychain-frontend/.yarn/releases .yarn/releases

COPY ./supplychain-frontend/apps/supply-chain ./apps/supply-chain
COPY ./supplychain-frontend/packages ./packages

RUN apk update

RUN apk add xsel

ARG REACT_APP_NODE_ADDRESS  \
    REACT_APP_CODE_ADDRESS
ENV REACT_APP_NODE_ADDRESS=${REACT_APP_NODE_ADDRESS} \
    REACT_APP_CODE_ADDRESS=${REACT_APP_CODE_ADDRESS} \
    DISABLE_ESLINT_PLUGIN=true

WORKDIR /supplychain-frontend/apps/supply-chain

RUN yarn install

RUN yarn build

RUN npm install --global serve

CMD ["serve", "-s", "/supplychain-frontend/apps/supply-chain/build"]
