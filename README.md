# BabyChimpGang (BCG)

Our one and only orginal BabyChimpGang NFT collection was released in December 2021. 1111 BabyChimps were minted in under 28 hours, making it one of the most successful NFT drops on the Fantom network at that time. 10% of the profits were donated to charity.

# BabyChimpGangXmas (BCGX)

Around Christmas 2021, in order to give back to the community, we airdropped the BabyChimpGangXmas collection to all BCG holders. 

# BCG Lottery
In April 2022, the BCG Lottery was held. More than 30 prizes, such as NFTs provided by other Fantom projects and BCG merchandise were raffled among ticked holders. The main prizes were the **BabyChimpGangHeroes**, a collection of 5 animated BabyChimps with superpowers. In total there were 5 different sets of tickets, each an NFT collection of their own with their own respective contracts and art on IPFS. Each original BCG or BCGX holder could also claim as many free tickets as she holded BCG or BCGX.
To make this work we have a public function 
```solidity
  function claimTickets() public {...}
````
in the respective contracts of each distinct set of Lottery tickes.  

At call, the function for lottery ticket set $0 \leq i < n $ automatically iterates through $ \[ id \mid id \equiv i \pmod{n} \]$ with id in the set of BCG and BCGX token the holders has in her wallet and checks if this id was already claimed. If not set this id to claimed and mint a free lottery ticket of ticket set i to the adress.  
(using only $ id $ for which hold $id \equiv i \pmod{n} $ for lottery ticket sets $i$ ensures the mutual exclusivity of the claimed chimps in the different lottery tickets sets. So no chimp can be claimed at multiple ticket sets. This way we don't need to keep track about that in an additional contract or with non-trivial intra contract communication.)

# Banana Token
In April 2022 we launched our Banana Token ($BNA), the utility token of BCG, which was airdropped to all BCG NFT holders, no matter which collection. Starting with the 1st of April 2022, holders of our NFTs collections will get $BNA airdropped the same amount every quarter. For more information check out  our Blue Paper in the respective Folder.

To ensure that no more than the intended total supply of $BNA will ever be in circulation, we added 
```solidity
require(totalSupply() +  amount  <= MAX_TOKENS, 'Would exceed max supply.');
```
to each minting function in the respective Banana Token contract.

# BabyChimpGangEvos (BCGE)
Launching in May 2022, holders of the original BCG collection have the possibility of evolving their BabyChimps into a mutant-apocalyptic style BabyChimp with the same attributes as the original one but in an evolved/mutated way. Half of the collection amount are available for the public mint/non BCG-holders.

 
For the evolution to be smooth we set the evolved chimp of every BCG to the same tokenID. That means when you evolve your BCG Chimo you get the BCGE Chimp with the same tokenID. Functions 
```solidity 
function evolveChimp(uint256 id) public payable {...)
function evolveMultipleChimps(uint256[] calldata id) public payable {...}
function evolveAllChimps() public payable {...}
```
basically check how many chimps of the one chimp, respective an array of chimps, respective all your chimps are not already evolved, and then evolves all the unevolved chimps in the selection, if the payment is $ n * $ MUTATION_PRICE for $ n = $ amount of unevolved chimps in selection. (Note: Of course one can only evolve their chimps and this will be checked in each of these functions.)  
To get the amount of unevovled chimps n in every selection of id's, the function
```solidity 
 function checkEvolve(uint256[] calldata id) external view returns (uint256){...}
```
can be used.

