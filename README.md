 
 ## PoWEth Token 
 [Deployed on Ethereum]()
 
![PowEth_small]()

 
 #### An ERC20 token that is mined using PoW through a SmartContract 
  
  * No pre-mine 
  * No ICO
  * 100,000,000 tokens total
  * Difficulty target auto-adjusts with PoW hashrate
  * Rewards decrease as more tokens are minted 
  * Compatible with all services that support ERC20 tokens
  
  
   
 #### How does it work?
 
Typically, ERC20 tokens will grant all tokens to the owner or will have an ICO and demand that large amounts of Ether be sent to the owner.   Instead of granting tokens to the 'contract owner', all 0xbitcoin tokens are locked within the smart contract initially.  These tokens are dispensed, 50 at a time, by calling the function 'mint' and using Proof of Work, just like mining bitcoin.  Here is what that looks like: 


     function mint(uint256 nonce, bytes32 challenge_digest) public returns (bool success) {

       
        uint reward_amount = getMiningReward();

        
        bytes32 digest =  keccak256(challengeNumber, msg.sender, nonce );

         
        if (digest != challenge_digest) revert();

        //the digest must be smaller than the target
        if(uint256(digest) > miningTarget) revert();
     

         uint hashFound = rewardHashesFound[digest];
         rewardHashesFound[digest] = epochCount;
         if(hashFound != 0) revert();  //prevent the same answer from awarding twice

        balances[msg.sender] = balances[msg.sender].add(reward_amount);

        tokensMinted = tokensMinted.add(reward_amount);

        //set readonly diagnostics data
        lastRewardTo = msg.sender;
        lastRewardAmount = reward_amount;
        lastRewardEthBlockNumber = block.number;
        
        //start a new round of mining with a new 'challengeNumber'
         _startNewMiningEpoch();

          Mint(msg.sender, reward_amount, epochCount, challengeNumber );

       return true;

    }
 
 
As you can see, a special number called a 'nonce' has to be passed into this function in order for tokens to be dispensed.  This number has to fit a special 'puzzle' similar to a sudoku puzzle, and this is called Proof of Work.   To find this special number, it is necessary to run a mining program.  A miner exists for mining PowEth tokens and it can be downloaded here: 

https://github.com/


 

 




### Transfer ERC20 Tokens 
https://
 
 
 
 ----------
 
#### HOW TO TEST

npm install -g ethereumjs-testrpc  (https://github.com/ethereumjs/testrpc)
testrpc

truffle test
  

 
 
