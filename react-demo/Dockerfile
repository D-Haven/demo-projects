FROM node:13.12.0-alpine AS builder

WORKDIR /app

# add `/app/node_modules/.bin` to $PATH
ENV PATH /app/node_modules/.bin:$PATH
ENV CI=true

# install app dependencies
COPY package.json ./
COPY package-lock.json ./
RUN npm install

# add app
COPY . ./

RUN npm test --coverage
RUN npm run build

##########################################

FROM bloritsch/spa-server:1.0.0

COPY config.yaml ./
COPY --from=builder /app/build /www
