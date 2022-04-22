改寫erc20 token 並加上以下功能
1.水龍頭的(給予相應token)
2.點數設計

```solidity
pragma solidity ^0.8.3;


import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/ERC20.sol";


contract sampleToken is ERC20 {

    uint public amountAllowed = 1000000000000000000;
    constructor(string memory name, string memory symbol) ERC20(name, symbol) {
        _mint(msg.sender, 50000000 * (10 ** 18));
    }

   


    mapping(address => uint) public lockTime;

    //水龍頭且需固定時間
    function faucet (address requestor , uint amount) external {
        require(block.timestamp > lockTime[msg.sender], "lock time has not expired. Please try again later");
        _mint(requestor, amount);
        lockTime[msg.sender] = block.timestamp + 1 days;
    }




     //時間計算
     uint public limit ;

    function init () external {
        limit = block.timestamp ;
    }


    //時間到進行回收
    function check_time (address to , uint amount ) external {
        if(block.timestamp>limit+10000){
            transferFrom(msg.sender, to,  amount) ;
        }
    }

    //轉給他人
     function re_transferFrom (address to ) external {
        if(to != msg.sender){
            limit =  block.timestamp;
        }
    }
    

}

```
