# Contracts

Pillar Protocol consists for following set of contract. 

1. Pillar Token Contract
2. Pillar Vault Params Contract
3. Pillar Vault Proxy Contract
4. Pillar Vault Storage Contract
5. Pillar Vault Factory Contract

## Pillar Token Contract
Pillar Token is a standard ZRC-2 contract. The [Mint](https://github.com/PillarProtocol/Contracts/blob/9468b89120be5ac26024becc616692f389c10363/Pillar.scilla#L206) function is modified such that only **Pillar Vault Factory Contract** is able to mint the tokens. 

## Pillar Vault Factory
All vault are created using this contract. The contract consists of primary logic how vaults are operated. 

## Pillar Vaults Params
All params that can be updated by onchain governance are stored in the this contract. These params can be changed by passing a governance proposal. 

## Pillar Vaults Proxy
Major operations for the pillar protocol are accessed via proxy. It helps acheive upgradability. 

## Pillar Vault Storage
Vault data is stored here.



# Major upgrades
1. There is no need to pre-create vaults. They can be created on fly. The vaults are free to create at the start of pillar protocol, however it can be changed by governance. 
2. No mininum collateral required for creating the vault.
3. Vault addresses have been eliminated. All vaults are now referred using a number. 
4. No multiple approvals. In most of the cases, user can simply approve only once and start using pillar protocol. All operations like *Add Collateral*, *Mint Pillar*, *Repay Pillar* and *Liquidate Vault* are one step process.
5. Additional method of updating price in the price oracle is added. (Vault Proxy now logic of price oracle embedded in it).
6. Contract have been made governance compatible. Any robust governance model can simply act on Pillar Protocol.