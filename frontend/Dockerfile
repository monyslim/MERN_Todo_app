FROM node:18-alpine AS build_image
WORKDIR /home/app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 3000


## The Second build stage
FROM node:18-alpine AS prod_build

WORKDIR /home/app


COPY --from=BUILD_IMAGE /home/app/build/ /home/app/build/

COPY package.json .

# COPY .env .

RUN npm install -g serve 


CMD ["serve", "-s", "build"]