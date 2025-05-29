## Run this script to start db

```bash
docker run -d \
  --name mariadb-ecommerce \
  --network kind \
  -e MARIADB_DATABASE=full-stack-ecommerce \
  -e MARIADB_USER=ecommerceapp \
  -e MARIADB_PASSWORD=StrongPa55WorD \
  -e MARIADB_ROOT_PASSWORD=rootpassword \
  -p 3306:3306 \
  mariadb:10.6
```

## Run seed script

```bash
docker cp ./01-create-user.sql mariadb-ecommerce:/docker-entrypoint-initdb.d/
docker cp ./02-create-products.sql mariadb-ecommerce:/docker-entrypoint-initdb.d/
docker cp ./03-refresh-database-with-100-products.sql mariadb-ecommerce:/docker-entrypoint-initdb.d/
docker cp ./04-countries-and-states.sql mariadb-ecommerce:/docker-entrypoint-initdb.d/
docker cp ./05-create-order-tables.sql mariadb-ecommerce:/docker-entrypoint-initdb.d/

docker exec -it mariadb-ecommerce bash -c "for file in /docker-entrypoint-initdb.d/*.sql; do mysql -u root -prootpassword full-stack-ecommerce < \$file; done"
```
