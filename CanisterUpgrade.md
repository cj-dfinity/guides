# Upgradeability of canisters


Upgrading a canister is a common task, when code is updated and deployed, the canister is upgraded. There are a few things to consider before upgrading a canister:
- Could the upgrade cause data loss?
- Could the upgrade break the dapp due to Candid changes?

## Preserving state (data)
When a canister is upgraded, the state is lost by default. This means all data application data will be lost, unless it's handled to persist when the canister is upgraded. This can be achieved by storing the data in stable variables, which will persist upgrades.





## Candid changes





Braking changes








## Upgrade vs. Reinstall

In some cases, 
