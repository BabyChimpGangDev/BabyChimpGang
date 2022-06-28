# BabyChimpGang (BCG)

Our one and only orginal **BabyChimpGang** NFT collection was released in December 2021. 1111 BabyChimps were minted in under 28 hours, making it one of the most successful NFT drops on the Fantom network at that time. 10% of the profits were donated to charity.

[Check out the deployed contract on FTMScan](https://ftmscan.com/address/0x7f9893ef9726d23e249518eaa1424677b7fed6a9)

# BabyChimpGangXmas (BCGX)

Around Christmas 2021, in order to give back to the community, we airdropped the **BabyChimpGangXmas** collection to all BCG holders. 

[Check out the deployed contract on FTMScan](https://ftmscan.com/address/0x207a1521aa373a9bd44c17faf9e77397195b77f9)

# BCG Lottery
In April 2022, the BCG Lottery was held. More than 30 prizes, such as NFTs provided by other Fantom projects and BCG merchandise were raffled among ticked holders. The main prizes were the **BabyChimpGangHeroes**, a collection of 5 animated BabyChimps with superpowers. In total there were 5 different sets of tickets, each an NFT collection on their own with their unique respective contracts and distributed art on IPFS. Each original BCG or BCGX holder could claim as many free tickets as she holded BCG or BCGX tokens.
To make this work we have a public function 
```solidity
function claimTickets() public {...}
````
in the respective contracts of each distinct set of Lottery tickes.  

At call, the function for lottery ticket set  $0 \leq i < 5 $ automatically iterates through $ \[ id \mid id \equiv i \pmod{5} \]$ for id in the set of BCG and BCGX token the holders has in her wallet and checks if this id was already claimed. If not set this id to claimed and mint a free lottery ticket of ticket set i to the adress.  
(using only $id $ for which  $id \equiv i \pmod{n} $ holds, for lottery ticket sets $i$ ensures the mutual exclusivity of the claimed chimps in the different lottery tickets sets. So only one ticket in one ticket set can be claimed for each chimp . This way we don't need to keep track about this in  additional contracts or with non-trivial intra contract communication.)

[Check out Lottery Ticket Set 1 on FTMScan](https://ftmscan.com/address/0x64b375f7c8f74e00dbc46e8497ae6dc90e3f3a01)  
[Check out Lottery Ticket Set 2 on FTMScan](https://ftmscan.com/address/0x1b7cf0279f47d973fd870d295f32e4b6a10f8958)  
[Check out Lottery Ticket Set 3 on FTMScan](https://ftmscan.com/address/0xac387c08ca418c7182f17cca957b863679ea3373)  
[Check out Lottery Ticket Set 4 on FTMScan](https://ftmscan.com/address/0x91b4b3e41c755ffb4656799f41bf7bc98e84dbf7)  
[Check out Lottery Ticket Set 5 on FTMScan](https://ftmscan.com/token/0x337d54327a75d39109d046f35c76960e6cd6099b)

[Check out the BabyChimpGangHeroes contract on FTMScan](https://ftmscan.com/address/0xb926ad1b2a331049a0f19ddd2f19e82988e4b854)

# Banana Token ($BNA)
In April 2022 we launched our **Banana Token**, the utility token of BCG, which was airdropped to all BCG NFT holders, no matter which collection. Starting with the 1st of April 2022, holders of our NFTs collections will get $BNA airdropped the same amount every quarter. For more information check out  our Blue Paper in the respective Folder.

To ensure that no more than the intended total supply of $BNA will ever be in circulation, we added 
```solidity
require(totalSupply() +  amount  <= MAX_TOKENS, 'Would exceed max supply.');
```
to each minting function in the respective Banana Token contract.

[Check out the deployed contract on FTMScan](https://ftmscan.com/address/0x132331815a1d519ca461e85949c8f2ed0feaece9)

# BabyChimpGangEvos (BCGE)
Launching in May 2022, holders of the original BCG collection have the possibility of evolving their BabyChimps into a mutant-apocalyptic style BabyChimp with the same attributes as the original one but in an evolved/mutated way. Half of the collection amount are available for the public mint/non BCG-holders.

 
For the evolution to be smooth we set the evolved chimp of every BCG to the same tokenID. That means when you evolve your BCG Chimp you get the BCGE Chimp with the same tokenID. Functions 
```solidity 
function evolveChimp(uint256 id) public payable {...)
function evolveMultipleChimps(uint256[] calldata id) public payable {...}
function evolveAllChimps() public payable {...}
```
basically check how many chimps of the one chimp, respective an array of chimps, respective all your chimps are not already evolved, and then evolves all the unevolved chimps in the selection, if the payment is  $n * $ MUTATION_PRICE, with  $n $ beeing the amount of unevolved chimps in the selection. (Note: Of course one can only evolve their chimps and this will be checked in each of these functions.)  
To get the amount of unevovled chimps  $n $ in every selection of id's, the function
```solidity 
 function checkEvolve(uint256[] calldata id) external view returns (uint256){...}
```
can be used.

[Check out the deployed contract on FTMScan](https://ftmscan.com/address/0x86645fe4975b03c7653eb3010ff78a02acc7acdc)

# RektChimpGang (BCGR)

For the first time on multichain, RektChimpGang launched for free on FTM and AVAX in the end of June 2022. 

This is also the first time we implemented an onchain lottery mechanism. With the function 
```solidty
function fundLottery() public payable {...}
```
one can fund the lottery with either FTM or AVAX (depending on chain).
The a call to function
```soldity
function drawLottery() public onlyOwner {...}
```
allows the owner to on-chain pseudorandomly select a holder of a Rekt Chimp and send him the previously funded amount in one transaction. 

For the pseudorandomnasly we rely on hashing the block difficulty, the block timestamp, and a counter with keccak256. The counter is very important in that it ensures that even if the function is executed in the same block and therefore timestamp and difficulty is the same, the result won't be the same. (Since the counter increases every time)
