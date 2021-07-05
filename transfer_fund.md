//SPDX-License-Identifier: Unlicense
pragma solidity ^0.8.6;

import "hardhat/console.sol";

contract avi_transferfund {

  address public owner;
  mapping (address => uint ) balances;

  constructor() payable  {
    owner = msg.sender;
    console.log("owner of the contract ",owner);
  }

  function send(address receiver) public payable {
    require( msg.value < 1 ether,"Ether exceeds allowed limit of 1 Eth");
    (bool success,bytes memory data) = receiver.call{value: msg.value}('');
    require(success == true, "Transfer failed.");
  }
  function contractBalance() view public onlyOwner returns (uint) {
    return address(this).balance;
  }

  modifier onlyOwner(){
    require(msg.sender == owner , "Not Owner");
    _;
  }
}