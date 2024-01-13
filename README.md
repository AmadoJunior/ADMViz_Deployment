##

## SSL

### Test:

```
docker compose run --rm certbot certonly --webroot --webroot-path /var/www/certbot/ --dry-run -d example.org
```

### Run:

```
docker compose run --rm certbot certonly --webroot --webroot-path /var/www/certbot/ -d example.org
```

### Renew: docker compose run --rm certbot renew

```
docker compose run --rm certbot renew
```
