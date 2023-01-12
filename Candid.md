# Candid Guide

## What is Candid
Candid is an interface describing the public services deployed in canisters on the Internet Computer. The Candid interface allows inter-operation between services, and between services and frontends, independently of the programming language used. 

The purpose of the Candid interface is similar to the purpose of a REST API, but where APIs typically use JSON to exchange data, Candid is an *Interface Description Language (IDL)*. IDL is platform and programming language neutral, and descibes the service, data formats, data structures etc. Read more about Candid in the [documentation](https://internetcomputer.org/docs/current/developer-docs/build/candid/candid-intro).

## DID-file
The Candid interface is automatically generated when building a Motoko project, but it can also be written manually. In its simplest form, the Candid DID-file contains a service description. The [Counter example dapp](https://github.com/dfinity/examples/tree/master/motoko/counter) is a good example of a minimalistic dapp, with a very small and simple Candid file. When the project is deployed, the counter.did file will contain this service description:

```json
service : {
  get: () -> (nat) query;
  inc: () -> ();
  set: (nat) -> ();
}
```






