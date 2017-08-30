# diverseiot-poc
Proof-of-concept demonstrator for DiverseIoT Phase 1

## Architecture

### Gateway
- C process communicating with some devices, should run on ARM (Raspberry Pi) or x86 (PC)

### "Cloud"-backend
- Java or NodeJS processes, parsing messages received from the Gateway
- Possibly C, if we want

### Communication
- Communication protocol: MQTT or Websocket
- Marshalling: Simple String or Simple Binary protocol

Each point above comes in two alternative, yielding 16 variants of the distributed system.

## Validation

- Write a simple scenario and define a simple oracle. Check that all variants pass the test.
- Sniff the network and comparare the traces for the 16 variants. Ideally, should be quite different. Exhibit some differences and some similarities (e.g. when using MQTT, it should be the same packet on the network whether we are using Java or JS, but it should look quite different when using WS, and it should look quite different between String/Binary serialization). Probably tools like Wireshark can help here.
- Profile CPU, dump memory, etc and compare traces for the 16 variants. Ideally, should be quite different. We should first identify some tools that can help here.
- compare "machine code". Well, it might not make sense for Java and JS... But, we could use LLVM to compare all the implementations (it is bindings for C, Java, NodeJS, maybe with different level of support) using the same intermediate representations. Then we could make the assumption that very different LLVM code yields very different behavior at the machine level, still having the same behavior (i.e. test passes)
