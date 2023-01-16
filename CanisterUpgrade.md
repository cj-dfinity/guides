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




## Candid changes





Braking changes








## Upgrade vs. Reinstall

In some cases, 
