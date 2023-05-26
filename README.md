kafka-fraud-detection
A Streaming Fraud Detection System that monitors user activity and flags the transaction as either legit or fraudulent using Kafka and Python.

Requirements:
Python: 3.10.4

Kafka: 1.3.5

Docker: 20.10.17

Considerations:
Because a fraud detection system relies on streamed data to produce alerts as soon as possible, Apache Kafka is used to handle the incoming data due to its streaming capabilities and the robust community surrounding this wonderful framework.

Architecture diagram:
Kafka diagram drawio

Two clusters are connected through a custom network labeled: kafka-network

The Source Cluster handles fraud detection
The Destination Cluster communicates the information processed by the Source Cluster and regulates processes through ZooKeeper
Project Layout:
To satisfy the architectural design, two Docker containers are used.

project_layout

Running the program:
First of all, we want to start the Destination Cluster first since it acts as the sink in this pipeline.

To spin up the Destination Cluster, run:

docker-compose -f docker-compose.kafka.yml build && docker-compose -f docker-compose.kafka.yml up

This is what be what the terminal should look like... kafka_container_output

Now, we need to spin up the Source Cluster to start feeding data to be processed.

Use this command to run the Source Cluster:

docker-compose build && docker-compose up

The Generator will then begin generating random source IDs, target IDs, and random amounts "spent".

generator_output

All transactions over $900 were marked as fraudulent by the Topic in the Source Cluster, so nothing over that amount should apear in the terminal. The data displayed below passed the fraudulent check and is being received by the Destination Cluster.

detector_output

That concludes the project!

Reflection:
Looking back, this was a great opportunity to learn about Kafka that utilized it in a reasonable example. I'm excited to apply this framework to problems that call for streamed data because to me, this is as live as data gets!

More logic can be applied to create a better fraud detection system, but that isn't the main focus for this project. Who knows, maybe I'll come back and implement a more advanced system :)
