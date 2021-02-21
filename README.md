# Contracts
Pillar Protocol implementation consists roughly 4 set of contracts.
1. Pillar Token Contract
2. Pillar Vault Factory Contract
3. Pillar Vault Contract
4. Price Oracle Contract


## Pillar Token Contract
Pillar Token is a standard ZRC-2 contract. The [Mint](https://github.com/PillarProtocol/Contracts/blob/9468b89120be5ac26024becc616692f389c10363/Pillar.scilla#L206) function is modified such that only **Pillar Vault Factory Contract** is able to mint the tokens. 

## Pillar Vault Factory Contract
Pillar Vault Factory is th e contract where all the Pillar Vaults are registered. The vaults can be created and [added](https://github.com/PillarProtocol/Contracts/blob/9468b89120be5ac26024becc616692f389c10363/VaultFactory.scilla#L190) only by vault factory admin. 
Any user can get a vault by calling [getNewVault](https://github.com/PillarProtocol/Contracts/blob/9468b89120be5ac26024becc616692f389c10363/VaultFactory.scilla#L221) transition.

## Pillar Vault Contract
Pillar Vault can be use to mint and burn Pillar Tokens.
Transition for minting Pillar Tokens: **MintPillar**
Transition for burning Pillar Tokens: **BurnPillar** or **RepayTotalDebt**

## Price Oracle Contract
Price Oracle is mainly used to provide prices of collateral to **Pillar Vault Contract**

# Stories

## Vault Factory
### Admin creates and adds a new vault.
1.  Admin of the Vault Creates by deploy a new instance [Vault contract](https://github.com/PillarProtocol/Contracts/blob/main/Vault.scilla).
2.  The address of the instance is [added to vault factory](https://github.com/PillarProtocol/Contracts/blob/9468b89120be5ac26024becc616692f389c10363/VaultFactory.scilla#L190) by admin.
3.  The Factory admin shall ensure that there are sufficient free vaults available.

### Transfer Factory Ownership
1. Factory admin/owner can [transfer the ownership](https://github.com/PillarProtocol/Contracts/blob/9468b89120be5ac26024becc616692f389c10363/VaultFactory.scilla#L174) of the vault factory to other address.  

### Deactivate Factory
1.  Vault Owner can chose to deactivate factory. Once the factory is deactivated a) no more vaults can be added to factory, b) no more pillar tokens can be minted.

### Get New Vault
Any user can get a new vault from a vault factory. Steps
1. On Pillar Token Contract user has to call [IncreaseAllowance](https://github.com/PillarProtocol/Contracts/blob/9468b89120be5ac26024becc616692f389c10363/Pillar.scilla#L226) transition `where spender is vaultFactory address`.
2. On Vault Factory contract call [getNewVault](https://github.com/PillarProtocol/Contracts/blob/9468b89120be5ac26024becc616692f389c10363/VaultFactory.scilla#L221) `where collateralAmount is the amount that will be put in vault post the vault is created` 


## Vault
### Borrow Pillar Tokens
The owner of the vault can borrow the Pillar Tokens from the vault using transition [MintPillar](https://github.com/PillarProtocol/Contracts/blob/9468b89120be5ac26024becc616692f389c10363/Vault.scilla#L609). The tokens minted are subjected to liquidation ratio and total debt.
