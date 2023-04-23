
# SQS Queue, DynameDB with LocalStack
Build AWS infrastructure with LocalStack enables faster local development without the need to incur infrastructure expenses, test AWS resource locally and debug locally

## Pre-requisites
To be able to up a AWS Infrastructure with Localstack, make sure you have docker installed, I'm using [this version](https://www.docker.com/products/docker-desktop/)

## Usage

## AWS Queue 
#### 1. Run docker-compose up an run the next steps:

#### 2. Create queue, just need put the of queue at {queue_name}
```awscli
awslocal --endpoint-url=http://localhost:4566 sqs create-queue --queue-name {queue_name}
```

#### 3. With this command you can list the queues that you have
```awscli
awslocal --endpoint-url=http://localhost:4566 sqs list-queues
```

#### 4. To send a message for a queue that you created, for run this command you need to alter {queue_name} for the same name of queue that you are created at the 2 step
```awscli
awslocal --endpoint-url=http://localhost:4566 sqs send-message --queue-url http://localhost:4566/000000000000/queue_name --message-body "Corpo da mensagem"
```

#### 5. To receive a message from the queue that you create
```awscli
awslocal --endpoint-url=http://localhost:4566 sqs receive-message --queue-url http://localhost:4566/000000000000/nome-da-fila
```

## DynamoDB

#### 1. Run docker-compose up an run the next steps:

#### 2. Create table
```awscli
awslocal dynamodb create-table \
    --table-name Order \
    --attribute-definitions \
        AttributeName=client_name,AttributeType=S \
        AttributeName=order,AttributeType=S \
    --key-schema \
        AttributeName=client_name,KeyType=HASH \
        AttributeName=order,KeyType=range \
    --provisioned-throughput \
        ReadCapacityUnits=5,WriteCapacityUnits=5 \
    --table-class STANDARD
    --region us-east-1
```

#### 3. List tables
```awscli
awslocal dynamodb list-tables --region us-east-1
```
#### 4. Put item
```awscli
awslocal dynamodb put-item \
    --table-name Order  \
    --item \
        '{"client_name": {"S": "manoel"}, "order": {"S": "teste2"}}'
```

#### 5. Get specific item
```awscli
awslocal dynamodb get-item --consistent-read \
    --table-name Order \
    --key '{ "client_name": {"S": "manoel"}, "order": {"S": "teste"}}'
```

#### 6. Query by name 
```awscli
awslocal dynamodb query \
    --table-name Order \
    --key-condition-expression "client_name = :name" \
    --expression-attribute-values  '{":name":{"S":"manoel"}}'
```