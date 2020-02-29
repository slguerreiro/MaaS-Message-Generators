# MaaS-Message-Generators
IE 2019/2020 MaaS Kafka Message Generators

Verify if JAVA 8 is available using the command: 

    java -version

Then, to execute the generator of Metro usage messages use the following command:

    java -jar MaaSMessageMetroGenerator.jar

The following options are available:
```
    MaaSMessageMetroGenerator --broker-list <KafkaBrokerList with Ports> --topic <topic> --token-list <token-list> --throughput <value> --typeMessage <value>
where, 
--broker-list: is a broker list with ports (e.g.: kafka02.example.com:9092,kafka03.example.com:9092) and the default value is localhost:9092
--topic: is the kafka topic to be provisioned and is mandatory
--token-list: is a list of client tokens (e.g.: eudij3674fgo,dhjsyuyfdhi3,djkfjd8) and is mandatory
--throughput: is the approximate maximum messages to be produced by minute and the default value is 10
--typeMessage: is the type of message to be produced: JSON or XML, default value is JSON.
```
Some examples of the messages sent in JSON:
{"Metro":{"CheckIn":{ "Token": "t2", "Station": "Odivelas", "Timestamp": "2020-02-29 18:23:41.278" }}}
{"Metro":{"CheckOut":{ "Token": "t2", "Station": "Alameda", "Timestamp": "2020-02-29 18:23:47.718" }}}

Some examples of the messages sent in XML:
Metro><CheckIn><Token>t1</Token><Station>Alto dos Moinhos</Station><Timestamp>2020-02-29 18:28:09.568</Timestamp></CheckIn></Metro>
<Metro><CheckOut><Token>t1</Token><Station>Campo Pequeno</Station><Timestamp>2020-02-29 18:28:09.876</Timestamp></CheckOut></Metro>
