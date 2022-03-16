# Kafka Play

Repository for playing with kafka CDC tooling.

## Setup

```bash
docker-compose up

# Start Postgres connector
curl -i -X POST -H "Accept:application/json" -H  "Content-Type:application/json" http://localhost:8083/connectors/ -d @register-postgres.json

# Consume messages from a Debezium topic
docker-compose exec kafka /kafka/bin/kafka-console-consumer.sh \
    --bootstrap-server kafka:9092 \
    --from-beginning \
    --property print.key=true \
    --topic dbserver1.inventory.customers

# Modify records in the database via Postgres client
docker-compose exec postgres env PGOPTIONS="--search_path=inventory" bash -c 'psql -U $POSTGRES_USER postgres'
```
