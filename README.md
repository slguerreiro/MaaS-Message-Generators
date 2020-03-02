# MaaS-Message-Generators
Enterprise Integration / IST - 2019/2020 MaaS Kafka Message Generators to be used in the project as simulator of clients performing actions in the MaaS (Mobility as a Service) platform.

Firstly, verify if JAVA 8 is available, on your linux environment, using the command: 

    java -version

Then, to execute the generator of metro usage messages use the following command:

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

The same applies to the generator of taxi usage messages:
```
java -jar MaaSMessageTaxiGenerator.jar
```    
where the same options are available:
```
MaaSMessageTaxiGenerator --broker-list <KafkaBrokerList with Ports> --topic <topic> --token-list <token-list> --throughput <value> --typeMessage <value>
where, 
--broker-list: is a broker list with ports (e.g.: kafka02.example.com:9092,kafka03.example.com:9092) and the default value is localhost:9092
--topic: is the kafka topic to be provisioned and is mandatory
--token-list: is a list of client tokens (e.g.: eudij3674fgo,dhjsyuyfdhi3,djkfjd8) and is mandatory
--throughput: is the approximate maximum messages to be produced by minute and the default value is 10
--typeMessage: is the type of message to be produced: JSON or XML, default value is JSON.
```

Finally, for the generator of bike usage messages:
```
java -jar MaaSMessageBikeGenerator.jar
```
where the same options are available:
```
MaaSMessageBikeGenerator --broker-list <KafkaBrokerList with Ports> --topic <topic> --token-list <token-list> --throughput <value> --typeMessage <value>
where, 
--broker-list: is a broker list with ports (e.g.: kafka02.example.com:9092,kafka03.example.com:9092) and the default value is localhost:9092
--topic: is the kafka topic to be provisioned and is mandatory
--token-list: is a list of client tokens (e.g.: eudij3674fgo,dhjsyuyfdhi3,djkfjd8) and is mandatory
--throughput: is the approximate maximum messages to be produced by minute and the default value is 10
--typeMessage: is the type of message to be produced: JSON or XML, default value is JSON.
```

Some examples of the messages received in a Kafka broker (sent in JSON format):
```
{"Metro":{"CheckIn":{ "Token": "t2", "Station": "Odivelas", "Timestamp": "2020-02-29 18:23:41.278" }}}
{"Metro":{"CheckOut":{ "Token": "t2", "Station": "Alameda", "Timestamp": "2020-02-29 18:23:47.718" }}}
{"Taxi":{"Usage":{ "Token": "t3", "Price": "70.51901", "Timestamp": "2020-02-29 19:45:58.638" }}}
{"Bike":{"Usage":{ "Token": "t1.4", "Distance": "13.553344", "Timestamp": "2020-02-29 20:57:10.294" }}}
```

Some examples of the messages received in a Kafka broker (sent in XML format):
```
<Metro>
 <CheckIn>
  <Token>t1</Token>
  <Station>Alto dos Moinhos</Station>
  <Timestamp>2020-02-29 18:28:09.568</Timestamp>
 </CheckIn>
</Metro>

<Metro>
 <CheckOut>
  <Token>t1</Token>
  <Station>Campo Pequeno</Station>
  <Timestamp>2020-02-29 18:28:09.876</Timestamp>
 </CheckOut>
</Metro>

<Taxi>
 <Usage>
  <Token>t2</Token>
  <Price>88.09835</Price>
  <Timestamp>2020-02-29 19:46:22.782</Timestamp>
 </Usage>
</Taxi>

<Bike>
 <Usage>
   <Token>t1.2</Token>
   <Distance>6.123504</Distance>
   <Timestamp>2020-02-29 20:57:30.276</Timestamp>
 </Usage>
</Bike>
```

Remark: the Metro app guarantees the consistency of the check-in/out movements accordingly with the following rules:
```
// If Check-In operation and Token is free then OK and mark token as used
// else if Check-out operation and Token is used then OK and mark token as free
// else NOK
```
