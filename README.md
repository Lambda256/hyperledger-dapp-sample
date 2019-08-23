## Instructions

Run the sample program of fabric-sdk-java by following the steps below

### Confirm Profile

Copy the configuration file `connection-profile-standard.yaml` from the SDK package to the current directory.

### Install jar package

We have pre-downloaded the java-sdk 1.2.0 version of the jar package, located in the `lib` directory.

`fabric-sdk-java-1.2.0-jar-with-dependencies.jar`: Contains fabric-sdk-java and all its dependencies.
`fabric-sdk-java-1.2.0-sources.jar`: Contains the source code for fabric-sdk-java.


Run the following command to install the jar package to the local maven repository:
```
Mvn install:install-file -Dfile=./lib/fabric-sdk-java-1.2.0-jar-with-dependencies.jar -DgroupId=org.hyperledger.fabric-sdk-java -DartifactId=fabric-sdk-java -Dversion=1.2.0 -Dpackaging=jar
```

If you need to read the fabric-sdk-java source, you can install the source package:

```
Mvn install:install-file -Dfile=./lib/fabric-sdk-java-1.2.0-sources.jar -DgroupId=org.hyperledger.fabric-sdk-java -DartifactId=fabric-sdk-java -Dversion=1.2 .0 -Dpackaging=jar -Dclassifier=sources
```

### Deploying chain code

Upload `sacc.out` from the chaincode directory to the BaaS platform and complete the installation and instantiation steps. For details, please refer to: https://help.aliyun.com/document_detail/85739.html

### Open project

Open any IDE and import java project

Modify the contents of the `java-sdk-demo/src/main/java/com/aliyun/baas/Main.java` file to match your configuration.

```java
    Private static String channelName = "first-channel"; // channel name
    Private static String userName = "user1"; // username
    Private static String secret = "password"; // password
```

Execute the Main program.


Copy the configuration file `connection-profile-standard.yaml` from the SDK package to the current directory.


```shell
mvn compile
mvn exec:java -Dexec.mainClass="Main"  -Dexec.classpathScope=runtime -Dexec.cleanupDaemonThreads=false
```

## Sample Program Description

The sample program does the following:

1. Enroll user
2. Read the configuration file, connect to the channel-related peer, and listen for block events.
3. Get the block information of the ledger and output
4. Call the sacc smart contract, modify the ledger, and read
5. Disconnect the peer

## operation result

If the sample program runs successfully, you can observe output information similar to the following:


```
11:05:14,362 INFO  - Main              - =============================================================
11:05:14,418 INFO  - ChaincodeExecuter - [√] Got success response from peer peer2.aliorg.aliyunbaas.com:31121 => payload: 235
11:05:14,418 INFO  - ChaincodeExecuter - [√] Got success response from peer peer1.aliorg.aliyunbaas.com:31111 => payload: 235
11:05:14,418 INFO  - ChaincodeExecuter - Sending transaction to orderers...
11:05:16,976 INFO  - Main              - Receive block event (number 16) from Peer{ id: 5, name: peer1.aliorg.aliyunbaas.com:31111, channelName: testchannel01, url: grpcs://peer1.aliorg.aliyunbaas.com:31111}
11:05:16,979 INFO  - Main              - Receive block event (number 16) from Peer{ id: 6, name: peer2.aliorg.aliyunbaas.com:31121, channelName: testchannel01, url: grpcs://peer2.aliorg.aliyunbaas.com:31121}
11:05:16,980 INFO  - ChaincodeExecuter - Orderer response: txid23197603990e6f8482e01ed6aeb1a9e6294b8937b9522f18f3474a5f7381c510
11:05:16,980 INFO  - ChaincodeExecuter - Orderer response: block number: 16
11:05:17,036 INFO  - ChaincodeExecuter - [√] Got success response from peer peer2.aliorg.aliyunbaas.com:31121 => payload: 235
11:05:17,036 INFO  - ChaincodeExecuter - [√] Got success response from peer peer1.aliorg.aliyunbaas.com:31111 => payload: 235
11:05:17,036 INFO  - Main              - =============================================================
11:05:17,088 INFO  - ChaincodeExecuter - [√] Got success response from peer peer2.aliorg.aliyunbaas.com:31121 => payload: 882
11:05:17,089 INFO  - ChaincodeExecuter - [√] Got success response from peer peer1.aliorg.aliyunbaas.com:31111 => payload: 882
11:05:17,089 INFO  - ChaincodeExecuter - Sending transaction to orderers...
11:05:19,351 INFO  - Main              - Receive block event (number 17) from Peer{ id: 5, name: peer1.aliorg.aliyunbaas.com:31111, channelName: testchannel01, url: grpcs://peer1.aliorg.aliyunbaas.com:31111}
11:05:19,354 INFO  - Main              - Receive block event (number 17) from Peer{ id: 6, name: peer2.aliorg.aliyunbaas.com:31121, channelName: testchannel01, url: grpcs://peer2.aliorg.aliyunbaas.com:31121}
11:05:19,354 INFO  - ChaincodeExecuter - Orderer response: txidffdaf80944641184175a0506460cffa3bda21200f477a4b853bed546c3326338
11:05:19,354 INFO  - ChaincodeExecuter - Orderer response: block number: 17
11:05:19,414 INFO  - ChaincodeExecuter - [√] Got success response from peer peer2.aliorg.aliyunbaas.com:31121 => payload: 882
11:05:19,414 INFO  - ChaincodeExecuter - [√] Got success response from peer peer1.aliorg.aliyunbaas.com:31111 => payload: 882
11:05:19,414 INFO  - Main              - Shutdown channel.
11:05:19,420 INFO  - org.hyperledger.fabric.sdk.Channel - Channel testchannel01 eventThread shutting down. shutdown: true  thread: pool-1-thread-1
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  10.747 s
[INFO] Finished at: 2019-07-17T11:05:19+08:00
[INFO] ------------------------------------------------------------------------
```

## Problem Diagnosis

1. Error example: send proposal timeout failed

```
20:23:45,728 ERROR - org.hyperledger.fabric.sdk.Channel - Channel Channel{id: 1, name: testchannel01} sending proposal with transaction 45bb66f204d45c19b36b4d0d2cc2871c6f2bf33c309961960364eda05b0a1e99 to Peer{ id: 5, name: peer1.aliorg.aliyunbaas.com:31111, channelName: testchannel01, url: grpcs://peer1.aliorg.aliyunbaas.com:31111} failed because of timeout(6000 milliseconds) expiration
java.util.concurrent.TimeoutException: Waited 6000 milliseconds for io.grpc.stub.ClientCalls$GrpcFuture@b660793[status=PENDING, info=[GrpcFuture{clientCall={delegate={delegate=ClientCallImpl{method=MethodDescriptor{fullMethodName=protos.Endorser/ProcessProposal, type=UNARY, idempotent=false, safe=false, sampledToLocalTracing=true, requestMarshaller=io.grpc.protobuf.lite.ProtoLiteUtils$MessageMarshaller@7fd71cf, responseMarshaller=io.grpc.protobuf.lite.ProtoLiteUtils$MessageMarshaller@4f796e35, schemaDescriptor=org.hyperledger.fabric.protos.peer.EndorserGrpc$EndorserMethodDescriptorSupplier@5a101a3}}}}}]]
	at com.google.common.util.concurrent.AbstractFuture.get(AbstractFuture.java:471)
	at org.hyperledger.fabric.sdk.Channel.sendProposalToPeers(Channel.java:4108)
	at org.hyperledger.fabric.sdk.Channel.sendProposal(Channel.java:4032)
	at org.hyperledger.fabric.sdk.Channel.sendTransactionProposal(Channel.java:3915)
	at ChaincodeExecuter.executeTransaction(ChaincodeExecuter.java:93)
	at Main.executeChaincode(Main.java:107)
	at Main.main(Main.java:85)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.codehaus.mojo.exec.ExecJavaMojo$1.run(ExecJavaMojo.java:282)
	at java.lang.Thread.run(Thread.java:748)
```

```
20:23:45,734 WARN  - ChaincodeExecuter - [×] Got failed response from peer peer1.aliorg.aliyunbaas.com:31111 => FAILURE: Channel Channel{id: 1, name: testchannel01} sending proposal with transaction 45bb66f204d45c19b36b4d0d2cc2871c6f2bf33c309961960364eda05b0a1e99 to Peer{ id: 5, name: peer1.aliorg.aliyunbaas.com:31111, channelName: testchannel01, url: grpcs://peer1.aliorg.aliyunbaas.com:31111} failed because of timeout(6000 milliseconds) expiration
```

If you encounter an error similar to the above, the possible causes include a timeout between the client application and the peer service of the fabric network. The solution can be considered:
- Check network connectivity between client applications and fabric network peer services
- If the connection is over an external network or the network has a high latency, consider adjusting the `waitTime` value in `ChaincodeExecuter.java`

## Reference link
- [fabric-sdk-java official](https://github.com/hyperledger/fabric-sdk-java)
- [sdk-java maven repository](http://central.maven.org/maven2/org/hyperledger/fabric-sdk-java/fabric-sdk-java/1.2.0/)


