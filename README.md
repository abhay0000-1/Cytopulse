// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;


contract Project {
string public projectName;
address public owner;
uint256 public totalFunds;


mapping(address => uint256) public contributions;


constructor(string memory _name) {
projectName = _name;
owner = msg.sender;
}


// Contribute ETH to the project
function contribute() external payable {
require(msg.value > 0, "Contribution must be greater than 0");
contributions[msg.sender] += msg.value;
totalFunds += msg.value;
}


// Withdraw funds (only owner)
function withdraw(uint256 amount) external {
require(msg.sender == owner, "Only owner can withdraw");
require(amount <= address(this).balance, "Insufficient balance");
payable(owner).transfer(amount);
}


// Get contribution of a user
function getContribution(address user) external view returns (uint256) {
return contributions[user];
}
}
