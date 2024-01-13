FROM nginx:latest

# Install gettext for envsubst
RUN apt-get update && apt-get install -y gettext-base

# Copy Templates
COPY proxyServer.conf /etc/nginx/sites-available/${APP_DOMAIN}.template.conf

#Replace ENV
RUN envsubst < /etc/nginx/sites-available/${APP_DOMAIN}.template.conf > /etc/nginx/sites-available/${APP_DOMAIN}.conf

#Activate Site
RUN ln -s /etc/nginx/sites-available/${APP_DOMAIN}.conf /etc/nginx/sites-enabled/

# Start NGINX
ENTRYPOINT ["nginx ","-g","'daemon off;'"]