kafka-fraud-detection
A Streaming Fraud Detection System that monitors user activity and flags the transaction as either legit or fraudulent using Kafka and Python.

Requirements:
Python: 3.10.4

Kafka: 1.3.5

Docker: 20.10.17

Considerations:
Because a fraud detection system relies on streamed data to produce alerts as soon as possible, Apache Kafka is used to handle the incoming data due to its streaming capabilities and the robust community surrounding this wonderful framework.

#Architecture diagram:See architecture file
![Architecture](https://github.com/johan1704/Ineuron/assets/68570240/607c9032-7986-4e78-94d6-fcc35a40b710)


Two clusters are connected through a custom network labeled: kafka-network

The Source Cluster handles fraud detection
The Destination Cluster communicates the information processed by the Source Cluster and regulates processes through ZooKeeper
Project Layout:
To satisfy the architectural design, two Docker containers are used.

![111](https://github.com/johan1704/Ineuron/assets/68570240/dcd4bff8-975d-445a-bb31-d8b87ffb3f51)

project_layout

Running the program:
First of all, we want to start the Destination Cluster first since it acts as the sink in this pipeline.

To spin up the Destination Cluster, run:

docker-compose -f docker-compose.kafka.yml build && docker-compose -f docker-compose.kafka.yml up

This is what be what the terminal should look like... kafka_container_output<img width="757" alt="222" src="https://github.com/johan1704/Ineuron/assets/68570240/ff777fcf-5a6d-480a-9041-20bf962880fc">



Now, we need to spin up the Source Cluster to start feeding data to be processed.

Use this command to run the Source Cluster:

docker-compose build && docker-compose up

The Generator will then begin generating random source IDs, target IDs, and random amounts "spent".

<img width="756" alt="189238459-cbe5c632-5ede-4e8c-8972-98579c05280d" src="https://github.com/johan1704/Ineuron/assets/68570240/2bf169dd-036e-4fcf-85f8-7d0837cc7f32">

All transactions over $900 were marked as fraudulent by the Topic in the Source Cluster, so nothing over that amount should apear in the terminal. The data displayed below passed the fraudulent check and is being received by the Destination Cluster.

<img width="659" alt="189238925-5fdaee5d-0da3-4e76-a529-d5b8f9a671d9" src="https://github.com/johan1704/Ineuron/assets/68570240/34cadf83-dce3-4a02-96db-e2de3899b163">


That concludes the project!

Reflection:
Looking back, this was a great opportunity to learn about Kafka that utilized it in a reasonable example. I'm excited to apply this framework to problems that call for streamed data because to me, this is as live as data gets!

More logic can be applied to create a better fraud detection system, but that isn't the main focus for this project. Who knows, maybe I'll come back and implement a more advanced system :)
