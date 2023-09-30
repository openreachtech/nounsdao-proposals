# Add a Dynamic Reserve Price for the Auctions

Hello, we are the founding and operating members of the Japanese-speaking sub-DAO, [pNouns](https://pnouns.wtf/), (owning Noun #553/#556), and the members of [Crypto Learning Club (CLC)](https://cryptolearningclub.org/), (owning Noun #605/#606).

## TL;DL
- Observing the stagnant winning bids for #853 / #854 / #855 auctions (just under 20ETH), it is evident that the current NFT auction system is likely to attract even more arbitrageurs.
- The increase in arbitrageurs will lead to a stagnation in NounsDAO by strategically opposing any proposals made during the first fork.
- In order to continue the auctions while preventing the entry of arbitrageurs, we propose a contract to set the dynamic reserve price for NFT auctions at a value equal to or greater than the current pro-rata share of a single Noun = "the treasury at the start of the auction divided by the number of remaining NFTs."


**Note**

We propose this as a candidate proposal to start a discussion within the community. Any feedback is welcome. We will update the proposal documents [here](https://github.com/openreachtech/nounsdao-proposals). As for the future process, if there is enough support for adding a dynamic reserve price, we would like to update the candidate proposal and submit the implementation part as well.

## Structural Issues Facing NounsDAO
### What's Happening?
As of August 2023, the treasury wallet, managed on the smart contract, holds nearly 30,000 ETH as the operational fund for the DAO. These funds have been allocated to the roughly 10 proposals posted every week for various grants (ranging from tens to hundreds of ETH) to support branding activities for Nouns' automatically generated on-chain meme characters and to expand NounsDAO's "Nounish philosophy" worldwide. 

However, after the FTX incident in November 2022 and the subsequent decline in the NFT and blockchain market, the average price of a Noun, which was previously being auctioned for an average of 50-100 ETH per day, plummeted to 30-35 ETH.

As a result, by dividing the approximately 30,000 ETH pooled in the treasury wallet by the number of NFTs issued, and utilizing the commonly employed 'rage quit' function found in other DAOs, it became possible to liquidate Nouns when market conditions deteriorated. Recognizing this opportunity, arbitrageurs began to form a faction anticipating liquidation within NounsDAO to seek profit from the situation.

For this faction, the ETH accumulated in the treasury wallet translates to casting "Against" votes for any proposal that could potentially reduce the ETH they receive when liquidating their Nouns. As a result, NounsDAO's activities stagnated for nearly six months from early 2023 onwards.


In response to this, a solution arose from within the DAO, combining an on-chain forking mechanism with the “rage quit” function. Despite encountering some challenges along the way, this feature gained approval through on-chain voting, ultimately culminating in the first fork.

The majority of Nouns, along with the treasury wallet, sided with the faction anticipating liquidation. This resulted in the burning of the majority of Nouns, approximately 35 ETH was liquidated as the faction departed.

The holders that remain in the main NounsDAO own roughly 380 Nouns, sharing a belief in Nouns' long-term vision, along with a treasury wallet holding 13,000 ETH. The DAO was set for a fresh start.

However, recent signs indicate a looming issue. This is evident in the recent auctions, #853 / #854 / #855, where winning bids have dipped below 20 ETH each, once again creating an opportunity for arbitrageurs.

### A Possible Scenario by Doing Nothing
As of the time of writing this proposal, Noun NFTs have already been acquired by arbitrageurs (the user who won #854 has a history of past forks [Link to Etherscan](https://etherscan.io/address/0x67DaCc258DCCc8CbFB493c652ab5170C3CFf0AD9#nfttransfers)). With one Noun generated daily, there's a possibility of arbitrageurs putting in winning bids with an intention of liquidating Nouns, similar to the previous fork.

Without taking corrective action,  the on-chain voting mechanism of Nouns suggests that the faction expecting liquidation will likely vote against all proposals. Their aim is to prevent a reduction in the treasury wallet's amount for the next 100 to 200 days, which will lead to a stagnation in NounsDAO's operations ([This blog](https://mirror.xyz/cfeng.eth/8j9FljMPp2COKLovoHF6j9P1I_lSP-xzSh8QM8cw1iE) also provides insights into the impact of the forking mechanism on floor prices).


Therefore, we believe it's imperative to deliberate and implement appropriate measures before arbitrageurs potentially take control of NounsDAO.

## NFT Auctions as Fundraising
What’s the purpose of NFT auctions in NounsDAO?

For Nouns in its current state, setting aside its operational reality, it essentially boils down to conducting daily "fundraising" much like a startup. NounsDAO is raising funds from visionary individuals and pioneering companies worldwide, who anticipate the "future of a full-fledged DAO," at the brisk pace of one auction for a Noun per day.

During periods of high demand and enthusiasm for NFTs and cryptocurrencies, this daily pace may have been suitable for maintaining a balance between supply and demand. However, with the NFT market now experiencing the trough of disillusionment and diminishing expectations, continuing at this same fundraising pace carries the risk of entering a negative cycle, ultimately making NounsDAO vulnerable to arbitrageurs.


## Solution
### Consensus on the Future of NounsDAO
With the first fork period finished, NounsDAO needs to establish consensus across the entire DAO on the following matters and modify the format of NFT auctions to better suit the current circumstances. 

1. Continuing NFT issuance is equal to "fundraising,” from a financial perspective.
2. When the market is experiencing a downturn or lacks corresponding business revenue, the “NFT floor price” calculated from the market capitalization will decrease. or if there is no accompanying business revenue model, the "NFT floor price" derived from the market capitalization will decrease.
3. As the "NFT floor price" decreases, the risk of being targeted by strategic arbitrageurs will rise again.
4. Post-fork, NounsDAO still possesses a substantial reserve of 13,000 ETH for ongoing operations.
5. **Implement a change in the NFT auction format to completely eliminate external pressure from arbitrageurs (this is our proposal).**
6. Advance discussions to create a more effective fundraising mechanism for NounsDAO.

### Detailed Proposal Explanation
We will now provide a thorough explanation of the proposed changes:

By updating the `NounsAuctionHouse` contract, we aim to add a dynamic minimum reserve price for the auction. This minimum bid will be set at **a value equal to or greater than the current pro-rata share of a single noun**. The value will be calculated by the formula below.

**minimum bid price = the treasury amount at the start of the auction / the number of remaining Nouns NFTs**

Also the treasury amount will be the total sum of ETH, stETH, and USDC held by the DAO.

e.g., the minimum bid price as of writing this proposal would be 35.09ETH = 13,547 (ETH) / 386 

By determining a minimum bid based on the Treasury amount, it will not be possible to make purchases below the average Treasury amount, as is currently the case with auctions at around 20 ETH.

If no bids are placed above the minimum reserve price, the Nouns NFTs will be burned. The total number of NounsNFTs and the total amount of treasury will remain the same, effectively having the same effect as if the auction had been stopped (i.e., preventing arbitrager purchases).

In cases where bids surpass the minimum reserve price, the user with the highest bid will receive the Nouns NFT, just as they did in current auctions. Since the winning bid exceeds the pro-rata share, it will increase the value of each Noun NFT. This influx of new users, who are not arbitrageurs, will stimulate the healthy growth of NounsDAO and elevate the value of Nouns NFTs.

### Anticipated Scenario with the Implementation of Minimum Reserve Price
Based on recent auction prices, it is expected that there will be a limited number of users willing to bid above the current pro-rata share of a single noun. Consequently, there will likely be a period of standstill in the auctions, with no notable increase in new NFT holders.

On a positive note, funding Nounish proposals from the treasury will still be viable, without concerns about arbitrageurs. This allows for a smooth processing of Nouns proposals as usual.

Given that it's shortly after the fork, it's presumed that not many arbitrageurs are left in the DAO. This, in turn, will enhance the intrinsic value of Nouns IP, and active funding for Nounish proposals will be made possible.

Moreover, with proactive funding, the overall amount in the treasury will gradually decrease, resulting in a reduction of the minimum reserve price. This, in turn, will attract new Nouns holders.

The post-fork challenge for NounsDAO lies in elevating the quality of proposals and exploring more effective ways to utilize the funds. With the introduction of the minimum reserve price based on the treasury, it becomes imperative to increase the number of users bidding above the average treasury amount to acquire new Nouns holders. Therefore, it's crucial to take an active approach to using the treasury funds.

## Summary
This proposal may seem like a passive attempt to preserve the assets in the treasury. However, considering the current situation where there is an economic threat from external sources (arbitrageurs), it is natural to consider measures to prevent the stagnation of DAO activities and to eliminate external pressure for survival.

Furthermore, this proposal serves to clarify the original purpose of utilizing Nouns' treasury for Nounish proposals, rather than for the profit of arbitrageurs.

Decision-making for funding in a DAO is a complex matter, and while NounsDAO's structure shows promise, there is still room for improvement.

We believe that advancing discussions for creating a more effective funding mechanism for NounsDAO, all while mitigating external pressure from arbitrageurs, is a positive step forward.
