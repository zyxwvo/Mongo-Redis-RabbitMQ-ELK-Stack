# Node.js, MongoDB, Redis, Postgres, Kafka, ELK, and RabbitMQ Backend Project

## Table of Contents
- [Introduction](#introduction)
- [Features](#features)
  - [MongoDB](#mongodb)
  - [Redis-Mongo-Flow](#redis-mongo-flow)
  - [RabbitMQ](#rabbitmq)
  - [Apache Kafka](#apache-kafka)
  - [Round-Robin Load Balancing Algorithm](#round-robin-load-balancing-algorithm)
  - [ELK Stack](#elk-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Special Notes](#special-notes)
- [Live Deployment](#live-deployment)
- [Test Statuses](#test-statuses)
- [Recommended GUI Tools](#recommended-gui-tools)
- [License](#license)
- [Author](#author)

## Introduction

This project is a sample, demo Node.js Backend project that demonstrates how to connect to **MongoDB, Redis, PostgreSQL, Kafka, ELK-stack, and RabbitMQ.** It demonstrates how these services can be used and interact with each other in a Node.js application.

Additionally, the project demonstrates how to use the ELK stack (Elasticsearch, Logstash, Kibana) for logging, as well as how to implement a round-robin load-balancing algorithm using Redis.

And we call this the **NMRPKER-Stack**! 🚀 (*Just for fun, though*)

## Features

### MongoDB
- **MongoDB**: The project connects to a MongoDB database and performs CRUD operations.
  - **Aggregation**: The project demonstrates how to use MongoDB's aggregation framework to perform complex queries, such as:
    - Grouping data by a field.
    - Filtering data based on a condition (lookup, match, project, etc.)
    - Sorting data.
    - Unwinding arrays.

### Redis-Mongo-Flow
- **Redis-Mongo-Flow**: The project also demonstrates how to use Redis as a cache layer for MongoDB.
  - This is done by first checking if the data exists in Redis. 
  - If it does, the data is retrieved from Redis. 
  - If it doesn't, the data is retrieved from MongoDB and stored in Redis.
  - This is done to reduce the number of queries to the database, thereby reducing the load on the database.

### RabbitMQ
- **RabbitMQ**: The project also demonstrates how to connect to RabbitMQ and publish and consume messages.
  - The project uses RabbitMQ to publish a message and consume it.
  - The message is published to a queue and consumed by a consumer.
  - This is done to demonstrate how to use RabbitMQ for asynchronous communication between services.

### Apache Kafka
- **Apache Kafka**: The project also demonstrates how to connect to Apache Kafka and produce and consume messages.
  - The project uses Apache Kafka to produce a message and consume it.
  - The message is produced to a topic and consumed by a consumer.
  - This is done to demonstrate how to use Apache Kafka for real-time data streaming.

### Round-Robin Load Balancing Algorithm
- **Round-Robin Load Balancing Algorithm**: The project also demonstrates how to use Redis to implement round-robin load balancing.
  - The project has two routes, `/api/test/route1` and `/api/test/route2`.
  - The project uses Redis to store the number of requests to each route.
  - The project uses round-robin load balancing to distribute the requests evenly between the two routes.

### ELK Stack
- **ELK Stack**: The project also demonstrates how to use the ELK stack (Elasticsearch, Logstash, Kibana) for logging.
  - The project uses Logstash to parse the log messages and send them to Elasticsearch.
  - Elasticsearch will then index the log messages for searching and analysis.
  - (Optional) You can also enhance the project by using Kibana to visualize the log data.

Here is a table of the features demonstrated in this project:

| Feature                              | Description                                                      |
|--------------------------------------|------------------------------------------------------------------|
| MongoDB                              | Connect to MongoDB and perform CRUD operations.                  |
| Redis-Mongo-Flow                     | Use Redis as a cache layer for MongoDB.                          |
| RabbitMQ                             | Connect to RabbitMQ and publish and consume messages.            |
| Apache Kafka                         | Connect to Apache Kafka and produce and consume messages.        |
| Round-Robin Load Balancing Algorithm | Implement round-robin load balancing using Redis.                |
| ELK Stack                            | Use the ELK stack (Elasticsearch, Logstash, Kibana) for logging. |
| PostgreSQL                           | Connect to PostgreSQL and perform CRUD operations.               |
| Express.js                           | Use Express.js as the web server framework.                      |
| Node.js                              | Use Node.js as the runtime environment.                          |
| JavaScript                           | Use JavaScript as the programming language.                      |
| NPM                                  | Use NPM as the package manager.                                  |
| REST API                             | Use REST API for communication.                                  |

## Project Structure

The project has the following structure:

```
node-mongo-redis-project
├── index.js             # Main entry point for the project for testing the connections
├── config.js            # Configuration file for the project
├── package.json         # NPM package file
├── publish.js           # Script to publish a message to RabbitMQ
├── README.md
├── apache-kafka
│   └── kafkaService.js  # Core logic for Apache Kafka
├── round-robin
│   ├── index.js         # Core logic for round-robin load balancing & for testing the algorithm
│   └── config.js        # Configuration file for Redis
├── routes
│   └── test.js          # Sample routes for the project
├── redis-mongo-flow
│   ├── app.js           # Core logic of the Redis-Mongo flow
│   ├── config.js        # Configuration file for Redis and MongoDB         
│   ├── seed.js          # Script to populate MongoDB with sample data
│   └── test.js          # Script to test the Redis-Mongo flow
├── elk-stack
│   └── index.js         # Core logic for logging using the ELK stack & testing the stack
└── postgresql
    └── app.js           # Core logic for PostgreSQL
    └── config.js        # Configuration file for PostgreSQL
```

## Getting Started
To **get started**, run the following commands:

1. Start the MongoDB service:
    ```bash
    brew services start mongodb-community
    ```

2. Start the Redis service:
    ```bash
    redis-server
    ```
   
3. Start the RabbitMQ service:
    ```bash
    brew services start rabbitmq
    ```
   
4. Start the Apache Kafka service:
    - First, navigate to the Kafka directory:
      ```bash
      cd kafka_2.13-3.8.0
      ```
    - Start the Zookeeper service:
        ```bash
        bin/zookeeper-server-start.sh config/zookeeper.properties
        ```
    - Start the Kafka service:
        ```bash
        bin/kafka-server-start.sh config/server.properties
        ```
   
5. `cd` back into the project directory (fix the path if necessary):
    ```bash
   cd node-mongo-redis-project
   ```
   
6. Start the Node.js server:
    ```bash
    node index.js
    ```
   
7. (Optional) Test the RabbitMQ service by publishing a message (go to another terminal window):
    ```bash
    node publish.js
    ```
   
   Verify that the message is received by the consumer by going to the terminal that is running the Node.js server (the one you started the index.js script).
   You should receive the following messages in the terminal:
   ```bash
    Server running on port 5000
    Visit http://localhost:5000/ to test the connection.
    Redis Connected
    MongoDB Connected
    Redis Test: Hello from Redis
    Kafka Producer and Consumer Connected
    Aggregation result: [
      { _id: 'Frank', totalOrderValue: 60 },
      { _id: 'David', totalOrderValue: 100 },
      { _id: 'Charlie', totalOrderValue: 35 },
      { _id: 'Grace', totalOrderValue: 75 },
      { _id: 'Alice', totalOrderValue: 50 },
      { _id: 'Bob', totalOrderValue: 80 },
      { _id: 'Ivy', totalOrderValue: 55 },
      { _id: 'Eve', totalOrderValue: 45 },
      { _id: 'Helen', totalOrderValue: 90 }
    ]
    Sent message to Kafka: Hello Kafka from Express!
    {
      topic: 'test-topic',
      partition: 0,
      value: 'Hello Kafka from Express!'
    }
    RabbitMQ Connected
    [*] Waiting for messages in task_queue. To exit press CTRL+C
    [x] Received 'This is a test message!'
    ```
   
8. Visit [http://localhost:5000/](http://localhost:5000/) to test the connections. 
   - You should see the message: **"Server is running! MongoDB, RabbitMQ, Kafka, and Redis connections established."** on the webpage.
   - Also test the API routes by visiting the following URLs: [http://localhost:5000/api/test/route1](http://localhost:5000/api/test/route1) and [http://localhost:5000/api/test/route2](http://localhost:5000/api/test/route2).

9. (Optional) Test the Round-Robin Load Balancing Algorithm:
    ```bash
    cd round-robin
    node index.js
    ```
   
10. (Optional) Test the ELK Stack:
    ```bash
    cd elk-stack
    node index.js
    ```

## Special Notes
**Note:** Before you get started, be sure to have the following installed on your machine by running the following commands (the following instructions are for MacOS):

1. Install Homebrew:
    ```bash
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```
   
2. Install MongoDB:
    ```bash
    brew tap mongodb/brew
    brew install mongodb-community
    ```
   
3. Install Redis:
    ```bash
    brew install redis
    ```
   
4. Install RabbitMQ:
    ```bash
    brew install rabbitmq
    ```
   
5. Install Apache Kafka:
   - Go to the [Apache Kafka website](https://kafka.apache.org/downloads) and download the latest version of Apache Kafka.
   - Currently, the most stable version is: **Scala 2.13 version: kafka_2.13-3.8.0.tgz**.
   - Extract the downloaded file to wherever you want to install Kafka on your machine.
   - Alternatively, you can use this direct link in your terminal to install Kafka:
     ```bash
     wget https://downloads.apache.org/kafka/3.8.0/kafka_2.13-3.8.0.tgz
     ```

6. Ensure Kafka is running:
   - First, navigate to the Kafka directory:
     ```bash
     cd kafka_2.13-3.8.0
     ```
   - Start the Zookeeper service:
       ```bash
       bin/zookeeper-server-start.sh config/zookeeper.properties
       ```
   - Start the Kafka service:
       ```bash
       bin/kafka-server-start.sh config/server.properties
       ```
     
7. Install Postgres:
    ```bash
    brew install postgresql
    ```
   
   Start the Postgres service:
    ```bash
    brew services start postgresql
    ```
   
   Create a new database named `davidnguyen` (or any name you prefer - as long as you change the database credentials in the `postgresql/config.js` file):
    ```bash
    createdb davidnguyen
    ```
   
   Connect to the database:
    ```bash
    psql davidnguyen
    ```
   
9. Install Node.js:
    ```bash
    brew install node
    ```
   
10. Install NPM:
    ```bash
    brew install npm
    ```
   Then `cd` into the project directory and run:
    ```bash
    npm init -y
    ```
   
11. Install all the required packages:
    ```bash
    npm install
    ```
    
12. For Windows, refer to the official installation guides for [MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/), [Redis](https://redis.io/download), [RabbitMQ](https://www.rabbitmq.com/download.html), [Apache Kafka](https://kafka.apache.org/quickstart), and [PostgreSQL](https://www.postgresql.org/download/windows/).

## Live Deployment

This sample backend is also hosted on Render. You can check out the live demo here: [Node.js Backend Demo](https://mongo-redis-rabbitmq-kafka-elk-backend.onrender.com).

Feel free to explore the backend's routes and read the documentation at [`/docs`](https://mongo-redis-rabbitmq-kafka-elk-backend.onrender.com/docs/).

## Test Statuses
  [![MongoDB](https://img.shields.io/badge/MongoDB-Passed-brightgreen)](https://www.mongodb.com/)
  [![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Passed-brightgreen)](https://www.postgresql.org/)
  [![Redis](https://img.shields.io/badge/Redis-Passed-brightgreen)](https://redis.io/)
  [![RabbitMQ](https://img.shields.io/badge/RabbitMQ-Passed-brightgreen)](https://www.rabbitmq.com/)
  [![Apache Kafka](https://img.shields.io/badge/Apache%20Kafka-Passed-brightgreen)](https://kafka.apache.org/)
  [![ELK Stack](https://img.shields.io/badge/ELK%20Stack-Passed-brightgreen)](https://www.elastic.co/)
  [![REST API](https://img.shields.io/badge/REST%20API-Passed-brightgreen)](https://restfulapi.net/)
  [![Round-Robin Load Balancing Algorithm](https://img.shields.io/badge/Round--Robin%20Load%20Balancing%20Algorithm-Passed-brightgreen)](https://redis.io/)

## Recommended GUI Tools
- **MongoDB Compass**: A GUI tool for MongoDB that allows you to interact with your MongoDB databases.
- **RedisInsight**: A GUI tool for Redis that allows you to interact with your Redis databases.
- **RabbitMQ Management Plugin**: A plugin for RabbitMQ that provides a web-based management interface for RabbitMQ.
- **Kibana**: A GUI tool for Elasticsearch that allows you to visualize and analyze your data.
- **Postico**: A GUI tool for PostgreSQL that allows you to interact with your PostgreSQL databases.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

Feel free to use this project for your own learning purposes or as a reference for your own projects!

## Author
- **Son Nguyen** - [GitHub](https://github.com/hoangsonww)
- **Email**: [info@movie-verse.com](mailto:info@movie-verse.com)

---

Thank you for checking out this demo backend project! 🚀 Feel free to reach out if you have any questions or feedback. 😊
