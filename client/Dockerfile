#
# Build
#
FROM node:lts AS build

RUN apt-get update && apt-get install -y git

ARG GITHUB_FE_REPO_URL
ARG VITE_API_ENDPOINT
ARG NODE_ENV

RUN git clone ${GITHUB_FE_REPO_URL} /app

WORKDIR /app

RUN echo "VITE_API_ENDPOINT=${VITE_API_ENDPOINT}" > .env \
  && echo "NODE_ENV=${NODE_ENV}" >> .env

RUN npm cache clean --force && npm install

RUN npm run build

#
# Package
#
FROM nginx:latest

ARG APP_DOMAIN

WORKDIR /

# Install gettext for envsubst
RUN apt-get update && apt-get install -y gettext-base

COPY --from=build /app/dist/ /var/www/html/${APP_DOMAIN}

# Copy Templates
COPY ./staticServer.conf /

#Replace ENV
RUN envsubst \$APP_DOMAIN < /staticServer.conf > /etc/nginx/conf.d/${APP_DOMAIN}.conf

# Remove Template 
RUN rm /staticServer.conf