#
# Build
#
FROM node:lts AS build

RUN apt-get update && apt-get install -y git

ARG GITHUB_FE_REPO_PATH
ARG GIT_TOKEN
ARG VITE_API_ENDPOINT
ARG VITE_NODE_ENV
ARG RECAPTCHA_SITE

RUN git clone https://${GIT_TOKEN}@github.com${GITHUB_FE_REPO_PATH} /app

WORKDIR /app

RUN echo "VITE_API_ENDPOINT=${VITE_API_ENDPOINT}" > .env \
  && echo "VITE_NODE_ENV=${VITE_NODE_ENV}" >> .env \
  && echo "VITE_SITE_KEY=${RECAPTCHA_SITE}" >> .env

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

RUN rm /etc/nginx/conf.d/default.conf

#Replace ENV
RUN envsubst \$APP_DOMAIN < /staticServer.conf > /etc/nginx/conf.d/${APP_DOMAIN}.conf

# Remove Template 
RUN rm /staticServer.conf