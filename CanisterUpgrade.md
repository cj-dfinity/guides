# Upgradeability of canisters


Upgrading a canister is a common task, when code is updated and deployed, the canister is upgraded. There are a few things to consider before upgrading a canister:
- Could the upgrade cause data loss?
- Could the upgrade break the dapp due to Candid changes?

## Preserving state (data)
When a canister is upgraded, the state is lost by default. This means all data application data will be lost, unless it's handled to persist when the canister is upgraded. This can be achieved by storing the data in stable variables, which will persist upgrades, but stable variables does not support all data types.

### Stable types
Simple data types like Nat, Int and Text can be made stable variables, which mean their state will persist a canister upgrade, just by adding _stable_ to the declaration of the variable:

```
actor MyActor {

  stable var state : Int = 0;

  public func inc() : async Int {
    state += 1;
    return state;
  };
}
```
The value of the variable `state` will persist an upgrade, and not be lost.

### Non-stable types
More complex data types like Hashmap are not stable types. This doesn't mean their values can't persist after an upgrade, it just means their persistance must be handled manually. Fortunately the functions `` and `` 

```
actor MyActor {

  stable var entries : [(Text, Nat)] = [];

  let map = HashMap.fromIter<Text,Nat>(
    entries.vals(), 10, Text.equal, Text.hash);

  public func register(name : Text) : async () {
    switch (map.get(name)) {
      case null  {
        map.put(name, map.size());
      };
      case (?id) { };
    }
  };

  system func preupgrade() {
    entries := Iter.toArray(map.entries());
  };

  system func postupgrade() {
    entries := [];
  };
}
```
This code snippet shows how the state of a HashMap can persist an upgrade, by serializing the state data before the upgrade (`preupgrade()`). On the initialization of the `map` variable after the upgrade, the serialized state is loaded. This way the HashMap data is made pesistent after a canister upgrade. 


## Candid changes
Changes to a Motoko function may change the Candid interface, and that could potentially break the application. So when upgrading the canister, consider how the changes can impact the Candid interface. Even small changes to the Motoko code can have great impact on the Candid interface, and potentially break the dapp. Consider this example:

```
actor {
  stable var state : Int
};
```
In this example the variable `state` is an Int, but let's say in an update the type is changed to Nat, which is not a big change. 
```
actor {
  stable var state : Nat
};
```
This would be a breaking change for e.g. the client application if it expects an Integer. With this small change, the Candid interface will change.

## Data structure changes
Another example of how data can be lost, is by changing the data types. 

```
actor {
  stable var state : Int
};
```
In this example the variable `state` is an Int, but let's say in an update the type is changed to Text: 
```
actor {
  stable var state : Text
};
```
In this case the the current Int value will be lost. One way to avoid the data loss when changing the data types is to keep the original variable, and create a new variable for the new data type. This way the original data will not be lost due to canister upgrades.

## Upgrade vs. Reinstall

In some cases, especially for development, it may not be necessary to do a complete deploy of the code to test it. The DFX Reintall command will replace the code in the canister and delete all state data. Read more about Reinstalling canisters in the [documentation](https://internetcomputer.org/docs/current/developer-docs/build/project-setup/manage-canisters#reinstall-a-canister).


## Useful links
- [Verifying upgrade compatibility](https://internetcomputer.org/docs/current/developer-docs/build/cdks/motoko-dfinity/compatibility)
- [Managing Canisters](https://internetcomputer.org/docs/current/developer-docs/build/project-setup/manage-canisters#upgrade-a-canister)
- [Stable variables and upgrade methods](https://internetcomputer.org/docs/current/developer-docs/build/cdks/motoko-dfinity/upgrades)
- [Reinstall canisters](https://internetcomputer.org/docs/current/developer-docs/build/project-setup/manage-canisters#reinstall-a-canister)
