
## The Project covers following fetaures:
1. FastAPI health endpoint
2. Transaction API
3. PostgreSQL connection
4. Fraud scoring rules
5. Fraud alerts table
6. Basic ML model
7. React dashboard
8. Kafka streaming
9. Redis caching
10. Differential privacy
11. Federated learning simulation
12. Docker
13. Kubernetes
14. AWS + Terraform


## Dataset used is PaySim :
https://www.kaggle.com/datasets/ealaxi/paysim1/data

## Installations:
1. Docker:
a. brew install --cask docker-desktop
open docker desktop application and wait until it says docker is running
b. docker --version
c. docker compose version

2. NVM and Node:
a. curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.5/install.sh | bash
b. source ~/.zshrc
c. nvm install --lts
d. nvm alias default 'lts/*'
e. node --version
f. npm --version
g. nvm --version

3. Backend Packages:
a. python -m pip install --upgrade pip
b. pip install \
  fastapi \
  "uvicorn[standard]" \
  sqlalchemy \
  "psycopg[binary]" \
  alembic \
  pydantic-settings \
  python-dotenv
c. pip install \
  pytest \
  httpx \
  ruff


## What Kafka streaming does??
Kafka moves events between different parts of a system in real time.

Transaction generator / banking API
            ↓
Kafka topic: transaction-events
            ↓
Fraud detection service
            ↓
ML model calculates risk score
            ↓
Kafka topic: fraud-alerts
            ↓
PostgreSQL + dashboard + notification service

#### Without kafka:
Transaction API → Fraud service → Database → Notification service
#### With kafka:
Transaction API → Kafka
Kafka → Fraud service
Kafka → Database service
Kafka → Analytics service
Kafka → Notification service

In our project, the sequence can be,
transaction = save_transaction(data)
prediction = fraud_model.predict(transaction)
save_prediction(prediction)
publish_transaction_event(transaction)

Since your backend is Python, we do not initially need the Java Kafka Streams library. We need Kafka itself plus a Python producer and consumer.
Kafka tools,
1. Producers and consumers
2. Topics and partitions
3. Consumer groups
4. Message ordering
5. Offsets
6. Event replay
7. Delivery guarantees
8. Failure handling
9. Schema evolution
10. Why Kafka is better than a direct API call for a particular workflow

## Docker and Kuberenetes:
Docker:
"Package and run this application in a container."

Kubernetes:
"Run these containers, keep them healthy, scale them,
connect them, update them, and restart them if they fail."

Suppose the fraud-detection worker crashes.
Without Kubernetes, someone or another script must restart it.
With Kubernetes, it detects the failed container and starts a replacement.

## Redis
Redis is a very fast, in-memory data store. Instead of reading everything repeatedly from a slower database such as PostgreSQL, an application can keep frequently needed or temporary information in Redis.

#### Without redis:
Dashboard request
      ↓
FastAPI
      ↓
PostgreSQL query
      ↓
Calculate customer risk
      ↓
Return response

#### With Redis:
Dashboard request
      ↓
FastAPI
      ↓
Check Redis
   ↙       ↘
Found      Not found
  ↓            ↓
Return       Query PostgreSQL
quickly      and store in Redis

Redis supports more than basic key-value caching. It provides data structures such as strings, hashes, lists, sets, sorted sets and streams, making it useful for real-time applications.