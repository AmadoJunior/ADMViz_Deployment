## ENV Vars

#### Use 'sample.env' as a template to create application specific '.env' file.

### Build Step

```
docker compose build --no-cache
```

### Local Deploy

```
docker compose up -d
```

## SSL

### Test:

```
docker compose run --rm certbot certonly --webroot --webroot-path /var/www/certbot/ --dry-run -d example.org
```

### Run:

```
docker compose run --rm certbot certonly --webroot --webroot-path /var/www/certbot/ -d example.org
```

### Renew:

```
docker compose run --rm certbot renew
```
