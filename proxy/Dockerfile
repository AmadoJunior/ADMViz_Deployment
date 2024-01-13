FROM nginx:latest

WORKDIR /

# Install gettext for envsubst
RUN apt-get update && apt-get install -y gettext-base

ARG APP_DOMAIN

# Copy Templates
COPY ./proxyServer.conf /

#Replace ENV
RUN envsubst \$APP_DOMAIN < /proxyServer.conf > /etc/nginx/conf.d/${APP_DOMAIN}.conf

# Remove Template 
RUN rm /proxyServer.conf