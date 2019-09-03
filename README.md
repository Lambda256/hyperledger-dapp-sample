## Instructions

Run the sample program of fabric-sdk-java by following the steps below

### Confirm Profile

Copy the configuration file `connection-profile-standard.yaml` from the SDK package to the current directory.

### Install jar package

We have pre-downloaded the java-sdk 1.2.0 version of the jar package, located in the `lib` directory.

`fabric-sdk-java-1.4.0-jar-with-dependencies.jar`: Contains fabric-sdk-java and all its dependencies.
`fabric-sdk-java-1.4.0-sources.jar`: Contains the source code for fabric-sdk-java.


Run the following command to install the jar package to the local maven repository:
```
Mvn install:install-file -Dfile=./lib/fabric-sdk-java-1.2.0-jar-with-dependencies.jar -DgroupId=org.hyperledger.fabric-sdk-java -DartifactId=fabric-sdk-java -Dversion=1.2.0 -Dpackaging=jar
```

If you need to read the fabric-sdk-java source, you can install the source package:

```
Mvn install:install-file -Dfile=./lib/fabric-sdk-java-1.2.0-sources.jar -DgroupId=org.hyperledger.fabric-sdk-java -DartifactId=fabric-sdk-java -Dversion=1.2 .0 -Dpackaging=jar -Dclassifier=sources
```

### Open project

Open any IDE and import java project

Modify the contents of the `java-sdk-demo/src/main/java/com/lambda256/hledger/dapp/Main.java` file to match your configuration.

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
12:54:51,033 INFO  - com.lambda256.hledger.dapp.Main   - =============================================================
12:54:51,033 INFO  - com.lambda256.hledger.dapp.Main   - CA name: ca-org1
12:54:51,033 INFO  - com.lambda256.hledger.dapp.Main   - CA version: 1.4.2
12:54:51,034 INFO  - com.lambda256.hledger.dapp.Main   - Going to enroll user: admin
12:54:51,361 INFO  - com.lambda256.hledger.dapp.Main   - Enroll user: admin successfully.
12:54:52,755 INFO  - org.hyperledger.fabric.sdk.Channel - Channel Channel{id: 1, name: mychannel} eventThread started shutdown: false  thread: null 
12:54:52,755 INFO  - com.lambda256.hledger.dapp.Main   - =============================================================
12:54:52,759 INFO  - com.lambda256.hledger.dapp.Main   - Receive block event (number 5) from Peer{ id: 4, name: peer1.org1.example.com, channelName: mychannel, url: grpcs://rooin-6456326796789179455.luniverse.dev:8051}
12:54:52,760 INFO  - com.lambda256.hledger.dapp.Main   - Receive block event (number 5) from Peer{ id: 3, name: peer0.org1.example.com, channelName: mychannel, url: grpcs://rooin-6456326796789179455.luniverse.dev:7051}
12:54:52,816 INFO  - com.lambda256.hledger.dapp.Main   - Channel height: 6
12:54:52,834 INFO  - com.lambda256.hledger.dapp.Main   - Block #5 has previous hash id: a9e2e0af2a941080a9db52bac19fbd63be8ca6d11124e9f7661821bc04b17a43
12:54:52,834 INFO  - com.lambda256.hledger.dapp.Main   - Block #5 has data hash: 55153a1ea8ec64e2afa651b45eead1a1d266b3f4a3a350a5fe90ac9359a9b8be
12:54:52,837 INFO  - com.lambda256.hledger.dapp.Main   - Block #5 has calculated block hash is d61eac2db549db7f1453cee9370527481953972b27084e075fe21f8881a69cf1
12:54:52,859 INFO  - com.lambda256.hledger.dapp.Main   - Block #4 has previous hash id: 461793806fb096700dc960003a57de5ef2b37f7f617bab7bd770df63bbe7b234
12:54:52,860 INFO  - com.lambda256.hledger.dapp.Main   - Block #4 has data hash: aa2ee354eb79fd4ed5ce17a9f7a73e088b4670b78721d33c5d1cc61a25b6a178
12:54:52,860 INFO  - com.lambda256.hledger.dapp.Main   - Block #4 has calculated block hash is a9e2e0af2a941080a9db52bac19fbd63be8ca6d11124e9f7661821bc04b17a43
12:54:52,879 INFO  - com.lambda256.hledger.dapp.Main   - Block #3 has previous hash id: be503a6f98a51836d43b13ac1241a991903906e2920d701a8b80cd4588e82105
12:54:52,879 INFO  - com.lambda256.hledger.dapp.Main   - Block #3 has data hash: 278fc58e497ae16d2c57a610d2c58888a95815e3d61c7e299acfeff070c91a27
12:54:52,879 INFO  - com.lambda256.hledger.dapp.Main   - Block #3 has calculated block hash is 461793806fb096700dc960003a57de5ef2b37f7f617bab7bd770df63bbe7b234
12:54:52,897 INFO  - com.lambda256.hledger.dapp.Main   - Block #2 has previous hash id: 98f0728aebc5d54021800a949ce144a930539962e8d0bef33da44f19ba2d5f0b
12:54:52,897 INFO  - com.lambda256.hledger.dapp.Main   - Block #2 has data hash: 1744ee2fd367d5f5676b0c787559b4edd1e1be0098b8a7cea2eda22e29888ee5
12:54:52,897 INFO  - com.lambda256.hledger.dapp.Main   - Block #2 has calculated block hash is be503a6f98a51836d43b13ac1241a991903906e2920d701a8b80cd4588e82105
12:54:52,940 INFO  - com.lambda256.hledger.dapp.Main   - Block #1 has previous hash id: 57d5ab8ce8386d9b828006808c7cc0ce3bbb097faccef95c797ea53b11e0e942
12:54:52,940 INFO  - com.lambda256.hledger.dapp.Main   - Block #1 has data hash: cb57ea7543bcf6ea5bb35efea0dbbbf56e3ecaad99e3caa1df152bcfa8b2452b
12:54:52,940 INFO  - com.lambda256.hledger.dapp.Main   - Block #1 has calculated block hash is 98f0728aebc5d54021800a949ce144a930539962e8d0bef33da44f19ba2d5f0b
12:54:52,963 INFO  - com.lambda256.hledger.dapp.Main   - Block #0 has previous hash id: 
12:54:52,963 INFO  - com.lambda256.hledger.dapp.Main   - Block #0 has data hash: 268d02bb425cfe543440ed1c6080a2f5f37b9c8c3c2c3396a825be52022c3f72
12:54:52,963 INFO  - com.lambda256.hledger.dapp.Main   - Block #0 has calculated block hash is 57d5ab8ce8386d9b828006808c7cc0ce3bbb097faccef95c797ea53b11e0e942
12:54:52,963 INFO  - com.lambda256.hledger.dapp.Main   - =============================================================
12:54:53,010 INFO  - com.lambda256.hledger.dapp.ChaincodeExecuter - [√] Got success response from peer peer1.org1.example.com => payload: 
12:54:53,010 INFO  - com.lambda256.hledger.dapp.ChaincodeExecuter - [√] Got success response from peer peer0.org1.example.com => payload: 
12:54:53,010 INFO  - com.lambda256.hledger.dapp.ChaincodeExecuter - Sending transaction to orderers...
12:54:55,169 INFO  - com.lambda256.hledger.dapp.Main   - Receive block event (number 6) from Peer{ id: 4, name: peer1.org1.example.com, channelName: mychannel, url: grpcs://rooin-6456326796789179455.luniverse.dev:8051}
12:54:55,169 INFO  - com.lambda256.hledger.dapp.Main   - Receive block event (number 6) from Peer{ id: 3, name: peer0.org1.example.com, channelName: mychannel, url: grpcs://rooin-6456326796789179455.luniverse.dev:7051}
12:54:55,170 INFO  - com.lambda256.hledger.dapp.ChaincodeExecuter - Orderer response: txidacae6427d9116fd9acfd5b5aadc702b89ae1a8e085e243d51d24f48d9595f852
12:54:55,170 INFO  - com.lambda256.hledger.dapp.ChaincodeExecuter - Orderer response: block number: 6
12:54:55,194 INFO  - com.lambda256.hledger.dapp.ChaincodeExecuter - [√] Got success response from peer peer1.org1.example.com => payload: 140
12:54:55,194 INFO  - com.lambda256.hledger.dapp.ChaincodeExecuter - [√] Got success response from peer peer0.org1.example.com => payload: 140
12:54:55,218 INFO  - com.lambda256.hledger.dapp.ChaincodeExecuter - [√] Got success response from peer peer1.org1.example.com => payload: 160
12:54:55,219 INFO  - com.lambda256.hledger.dapp.ChaincodeExecuter - [√] Got success response from peer peer0.org1.example.com => payload: 160
12:54:55,219 INFO  - com.lambda256.hledger.dapp.Main   - Shutdown channel.
12:54:55,222 INFO  - org.hyperledger.fabric.sdk.Channel - Channel mychannel eventThread shutting down. shutdown: true  thread: pool-1-thread-1 
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


