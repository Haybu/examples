Examples
========

This repository includes projects demonstrating how to use the Java Kafka producer
and consumer. You can find detailed explanation of the code at the
[application development section](http://confluent.io/docs/current/app-development.html)
of the Confluent Platform documentation.

To build the producer project

    $ cd producer
    $ mvn clean package

To build the consumer project

    $ cd consumer
    $ mvn clean package

Quickstart
----------

Before running the examples, make sure that Zookeeper, Kafka and Schema Registry are
running. In what follows, we assume that Zookeeper, Kafka and Schema Registry are
started with the default settings.

    # Start Zookeeper
    $ bin/zookeeper-server-start config/zookeeper.properties

    # Start Kafka
    $ bin/kafka-server-start config/server.properties

    # Start Schema Registry
    $ bin/schema-registry-start config/schema-registry.properties

Then create a topic called page_visits:

    # Create page_visits topic
    $ bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 \
      --partitions 1 --topic page_visits

Next, cd to the `examples` directory:

    $ cd examples

First cd to the `producer` directory, then run the example producer to publish 10 records.

    # Run the producer
    $ cd producer
    $ mvn exec:java -Dexec.mainClass="io.confluent.examples.producer.ProducerExample" \
      -Dexec.args="10 http://localhost:8081"

Then cd to the `consumer` directory, and run the consumer group example to consume
the records we just published to the cluster and display in the console.

    # Run the consumer
    $ cd ../consumer
    $ mvn exec:java -Dexec.mainClass="io.confluent.examples.consumer.ConsumerGroupExample" \
      -Dexec.args="localhost:2181 group page_visits 1 http://localhost:8081"
