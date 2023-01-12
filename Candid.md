# Candid Guide

## What is Candid
Candid is an interface describing the public services deployed in canisters on the Internet Computer. The Candid interface allows inter-operation between services, and between services and frontends, independently of the programming language used. 

The purpose of the Candid interface is similar to the purpose of a REST API, but where APIs typically use JSON to exchange data, Candid is an *Interface Description Language (IDL)*. IDL is platform and programming language neutral, and descibes the service, data formats, data structures etc. Read more about Candid in the [documentation](https://internetcomputer.org/docs/current/developer-docs/build/candid/candid-intro).

## The DID-file
The Candid interface is automatically generated when building a Motoko project, but it can also be written manually. In its simplest form, the Candid DID-file contains a service description. The [Counter example dapp](https://github.com/dfinity/examples/tree/master/motoko/counter) is a good example of a minimalistic dapp, with a very small and simple Candid file. When the project is deployed, the `counter.did` file will contain this service description:

```
service : {
  get: () -> (nat) query;
  set: (nat) -> ();
  inc: () -> ();
}
```

The Counter dapp has three public functions: `get()`, `set(nat)` and `inc()`

From the service description we can see, that the get() function returns a number, and the service is a query function (faster execution). The set takes a number as an argument, but doesn't return anything, and inc() doesn't take an argument and doesn't return anything. 

See more advanced uses of Candid in the [documentation](https://internetcomputer.org/docs/current/developer-docs/build/candid/candid-concepts) or in other [Motoko examples](https://github.com/dfinity/examples/tree/master/motoko).




