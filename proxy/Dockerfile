FROM nginx:latest

WORKDIR /

# Install gettext for envsubst
RUN apt-get update && apt-get install -y gettext-base

ARG APP_DOMAIN
ARG API_HOST
ARG CLIENT_HOST

# Copy Templates
COPY ./proxyServer.conf /

RUN rm /etc/nginx/conf.d/default.conf

#Replace ENV
RUN envsubst \$APP_DOMAIN,\$API_HOST,\$CLIENT_HOST < /proxyServer.conf > /etc/nginx/conf.d/${APP_DOMAIN}.conf

# Remove Template 
RUN rm /proxyServer.conf