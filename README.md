# BabyChimpGang (BCG)

Our one and only oroginal BabyChimpGang NFT collection was released in December 2021. 1111 BabyChimps were minted in under 28 hours, making it one of the most successful NFT drops on the Fantom network at that time. 10% of the profits were donated to charity.

# BabyChimpGangXmas (BCGX)

Around Christmas 2021, in order to give back to the community, we airdropped the BabyChimpGangXmas collection to all BCG holders. 

# BCG Lottery
In April 2022, the BCG Lottery was held. More than 30 prizes, such as NFTs provided by other Fantom projects and BCG merchandise were raffled among ticked holders. The main prizes were the **BabyChimpGangHeroes**, a collection of 5 animated BabyChimps with superpowers. In total there were 5 different sets of tickets, each an NFT collection of their own with their own respective contracts and art on IPFS. Each original BCG or BCGX holder could also claim as many free tickets as she holded BCG or BCGX.
To make this work we have a public function 
```solidity
  function claimTickets() public {...}
````
in the respective contracts of each distinct set of Lottery tickes. At call, the function for lottery ticket set $m$ automatically iterates through $id \mod m : \forall id$ in the set of BCG and BCGX token the holders has in her wallet and checks if this id was already claimed. If not set this id to claimed and mint a free chimp to the adress. (using only & \{ id \mod m : \forall $ lottery tikcet sets $m \}$ ensures the mutual exclusion of the claimed chimps in the different lottery tickets sets. This way we don't need to keep track about that in an additional contract or with non-trivial intra contract communication.)

# Banana Token
In April 2022 we launched our Banana Token ($BNA), the utility token of BCG, which was airdropped to all BCG NFT holders, no matter which collection. Starting with the 1st of April 2022, holders of our NFTs collections will get $BNA airdropped the same amount every quarter. For more information check out  our Blue Paper in the respective Folder.

To ensure that no more than the intended total supply of $BNA will ever be in circulation, we added 
```solidity
require(totalSupply() +  amount  <= MAX_TOKENS, 'Would exceed max supply.');
```
to each minting function in the respective Banana Token contract.


# BabyChimpGangEvos (BCGE)
Launching in May 2022, holders of the original BCG collection have the possibility of evolving their BabyChimps into a mutant-apocalyptic style BabyChimp with the same attributes as the original one but in an evolved/mutated way. Half of the collection amount are available for the public mint/non BCG-holders. 

