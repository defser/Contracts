# Contracts
Pillar Protocol implementation consists roughly 4 set of contracts.
1. Pillar Token Contract
2. Pillar Vault Factory Contract
3. Pillar Vault Contract
4. Price Oracle Contract


## Pillar Token Contract
Pillar Token is a standard ZRC-2 contract. The Mint function is modified such that only **Pillar Vault Factory Contract** is able to mint the tokens. 

## Pillar Vault Factory Contract
Pillar Vault Factory is the contract where all the Pillar Vaults are registered. The vaults can be created and added only by vault factory admin. 
Any user can get a vault by calling **getNewVault** transition.

## Pillar Vault Contract
Pillar Vault can be use to mint and burn Pillar Tokens.
Transition for minting Pillar Tokens: **MintPillar**
Transition for burning Pillar Tokens: **BurnPillar** or **RepayTotalDebt**

## Price Oracle Contract
Price Oracle is mainly used to provide prices of collateral  
