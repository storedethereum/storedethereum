# Stored Ethereum

Stored Ethereum (STE) is an ERC-20 token that is designed to appreciate against ETH over time and reward long-term holders.

Stored Ethereum is completely decentralized and does not rely on stakers, oracles or other trusted parties. The contract logic is simple and open-source.

Each deposit and withdrawal increases the amount of ETH that can be redeemed per unit of STE in circulation. Your profit (in ETH) depends on the amount of ETH that is deposited and withdrawn after you minted STE. 

Stored Ethereum is deployed at [0x792F5bddE5F8cf4b075b7A9DC4f296341d00b0D1](https://etherscan.io/address/0x792F5bddE5F8cf4b075b7A9DC4f296341d00b0D1).

## How it works

You can mint STE by depositing ETH, and withdraw ETH by redeeming (i.e. burning) STE. Stored Ethereum has two features designed to gradually increase the amount of ETH that can be redeemed per unit of STE.

Let's define two terms:
- Contract balance: The total amount of ETH locked in the contract
- Total supply: The total amount of STE in circulation

### 1. Deposit fee

When you mint STE, 95% of your ETH deposit is used to mint STE. The remaining 5% is a deposit fee that rewards existing STE holders.

Each deposit increases the amount of ETH that can be redeemed per unit of STE in circulation.

`net_deposit = gross_deposit * 95%`

`tokens = total_supply * net_deposit/(contract_balance - net_deposit)`

`contract_balance` includes the current deposit.

*Special case: There is no deposit fee when total supply is zero.*

### 2. Withdrawal fee

When you redeem STE, 95% of your share of the contract balance is sent to you. The remaining 5% is a withdrawal fee that rewards remaining STE holders.

Each withdrawal increases the amount of ETH that can be redeemed per unit of STE in circulation.

`gross_withdrawal = contract_balance * tokens/total_supply`

`net_withdrawal = gross_withdrawal * 95%`

*Special case: There is no withdrawal fee when all tokens are redeemed.*

## Examples

- Let's assume an initial contract balance of `100 ETH` and a total supply of `100 STE`.

Deposit 1:
- Alice deposits `100 ETH`. The new contract balance is `100 ETH + 100 ETH = 200 ETH`.
- Her net deposit is `100 ETH * 95% = 95 ETH`.
- She receives `100 STE * 95 ETH/(200 ETH - 95 ETH) = 90 STE`.
- The new total supply is `100 STE + 90 STE = 190 STE`.

Deposit 2:
- Bob deposits `400 ETH`. The new contract balance is `200 ETH + 400 ETH = 600 ETH`.
- His net deposit is `400 ETH * 95% = 380 ETH`.
- He receives `190 STE * 380 ETH/(600 ETH - 380 ETH) = 328 STE`.
- The new total supply is `190 STE + 328 STE = 518 STE`.

Withdrawal 1:
- Bob withdraws `328 STE`.
- His gross withdrawal is `600 ETH * 328 STE/518 STE = 380 ETH`.
- He receives`380 ETH * 95% = 361 ETH`.
- The new contract balance is `600 ETH - 361 ETH = 239 ETH`.
- The new total supply is `518 STE - 328 STE = 190 STE`.

Withdrawal 2:
- Alice withdraws `90 STE`.
- Her gross withdrawal is `239 ETH * 90 STE/190 STE = 113 ETH`.
- She receives`113 ETH * 95% = 107 ETH`.
- The new contract balance is `239 ETH - 107 ETH = 132 ETH`.
- The new total supply is `190 STE - 90 STE = 100 STE`.

As we can see, Alice made a `107 ETH - 100 ETH = 7 ETH` profit. Bob withdrew right after depositing, which resulted in a `400 ETH - 361 ETH = 39 ETH` loss. Note that Bob's scenario is the worst case scenario. The Stored Ethereum contract will return at least `95% * 95% = 90.25%` of the ETH that was originally deposited.

Again: Your profit (or loss) depends on the incremental deposit and withdrawal volume after you minted STE.

*Numbers were rounded for clarity.*

## Economics

Minting STE is a bet that you're able to hold STE long enough to make a profit. Moreover, holding STE may discourage you from selling during an Ethereum bear cycle.

Widespread adoption of Stored Ethereum *may* increase the stability of Ethereum vs. fiat currencies as it disincentivizes short-term trading (this is not certain).

STE could be traded on a decentralized exchange or other form of secondary market. The STE/ETH exchange rate should be somewhere in between the withdrawable amount of ETH per 1 STE and the amount of ETH required to mint 1 STE.

STE could also be used as collateral just like ETH, because the amount of ETH that can be redeemed per unit of STE in circulation cannot decrease.

## Operation

Send ETH to the Stored Ethereum contract to mint STE. You may have to add the contract address to your wallet to see your STE tokens.

Call the `withdraw(uint wad)` method to withdraw ETH, where `wad` represents the amount of tokens to redeem (in wei).

Call the `withdrawable(address addr)` method to find out how much ETH can currently be withdrawn by a specified address.

Do not transfer STE to the contract address. This does not redeem your STE. Use the `withdraw(uint wad)` method to withdraw ETH.

## Disclaimer

Gas fees are not included in any of the calculations in this document.

Please ensure that you are sending ETH to the **correct contract address**! Websites and GitHub repos can be hacked.

Stored Ethereum is a crypto asset. Trading crypto assets carries a **high level of risk** and may not be suitable for all investors.

This is **not financial advice**. If you are unsure of any investment decision you should seek a professional financial advisor.

As per our best knowledge, this is **not a digital asset securities offering** as per the definition of the US Securities and Exchange Commission:
- The Ethereum distributed ledger network and the STE digital asset are fully developed and operational
- STE holders are immediately able to use STE for its intended functionality on the Ethereum network
- STE can be saved, retrieved and exchanged for a predictable amount of ETH at a later time

However, **you** are responsible for ensuring that trading Stored Ethereum is legal in your jurisdiction. This is not legal advice.

Stored Ethereum was carefully tested. Nevertheless, Stored Ethereum and this document is provided **without warranty of any kind**. See MIT license terms for details.
