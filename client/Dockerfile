#
# Build
#
FROM node:latest AS build

RUN apt-get update && apt-get install -y git

ARG GITHUB_FE_REPO_URL

RUN git clone ${GITHUB_FE_REPO_URL} /app

WORKDIR /app

RUN npm install

RUN npm run build

#
# Package
#
FROM nginx:latest

# Install gettext for envsubst
RUN apt-get update && apt-get install -y gettext-base

COPY --from=build /app/dist/ /var/www/html/${APP_DOMAIN}

# Copy Templates
COPY staticServer.conf /etc/nginx/sites-available/${APP_DOMAIN}.template.conf

#Replace ENV
RUN envsubst < /etc/nginx/sites-available/${APP_DOMAIN}.template.conf > /etc/nginx/sites-available/${APP_DOMAIN}.conf

#Activate Site
RUN ln -s /etc/nginx/sites-available/${APP_DOMAIN}.conf /etc/nginx/sites-enabled/

# Start NGINX
ENTRYPOINT ["nginx ","-g","'daemon off;'"]