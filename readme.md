
# SQS Queue with LocalStack
Build SQS Queue (Amazon SQS) with LocalStack, this enables faster local development without the need to incur infrastructure expenses.

## Pre-requisites
To be able to up a SQS Queue with localstack, make sure you have docker installed, I'm using [this version](https://www.docker.com/products/docker-desktop/)

## Usage

### 1. Run docker-compose up an run the next steps:

### 2. Create queue, just need put the of queue at {queue_name}
```awscli
awslocal --endpoint-url=http://localhost:4566 sqs create-queue --queue-name {queue_name}
```

### 3. With this command you can list the queues that you have
```awscli
awslocal --endpoint-url=http://localhost:4566 sqs list-queues
```

### 4. To send a message for a queue that you created, for run this command you need to alter {queue_name} for the same name of queue that you are created at the 2 step
```awscli
awslocal --endpoint-url=http://localhost:4566 sqs send-message --queue-url http://localhost:4566/000000000000/queue_name --message-body "Corpo da mensagem"
```

### 5. To receive a message from the queue that you create
```awscli
awslocal --endpoint-url=http://localhost:4566 sqs receive-message --queue-url http://localhost:4566/000000000000/nome-da-fila
```