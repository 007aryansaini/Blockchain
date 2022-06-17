// SPDX-License-Identifier: MIT
pragma solidity^0.8.0;

contract Lotter{

     address public immutable manager;
     address payable[] public players;



     constructor(){
         manager = msg.sender;
     }


     function alreadyEntered() view private returns(bool){
          for( uint i=0 ; i < players.length ; i++){
                if(  players[i] == msg.sender ){
                    return true;
                }
          }

          return false;
     }

     function participate() public payable{

              require( msg.sender != manager , "Manager cannot participate in lottery.");
              require(alreadyEntered() == false , "You cannot enter multiple times in the lottery.");
              require(msg.value >= 1 ether, "You must pay at least 1 ether to participate in lottery.");

              players.push(payable(msg.sender));

     }

     function random() view private returns(uint){
             return uint(sha256(abi.encodePacked(block.difficulty , block.number , players)));
     }

     function pickWinner() public {
            require(msg.sender == manager , "Only manager can choose the winner.");
            uint index = random() % players.length;
            players[index].transfer(address(this).balance);

           
            players = new address payable[](0);


            

     }

     


     function getPlayers() public view returns(address payable[] memory ){
         return players;
     }

     



}
