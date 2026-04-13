1. Build Docker image:

docker compose up -d --build

3. Chay php
docker compose exec php bash

2. Import DB
php bin/magento setup:install \
--base-url=http://localhost:8080 \
--db-host=localhost \
--db-name=magento \
--db-user=magento \
--db-password= magento \
--admin-firstname=admin \
--admin-lastname=admin \
--admin-email=abbbdmin@admin.com \
--admin-user=thanh \
--admin-password=thanh123 \
--language=en_AU \
--currency=AUD \
--search-engine=opensearch \
--opensearch-host=opensearch \
--opensearch-port=9200 \
--opensearch-index-prefix=magento2 \
--opensearch-enable-auth=0 \
--opensearch-timeout=15 \
--timezone=Australia/Sydney \
--use-rewrites=1

- Restart Service
docker compose restart nginx