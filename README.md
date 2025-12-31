// SPDX-License-Identifier: MIT
pragma solidity ^0.8.23;

contract SimpleContract {

    address private _owner;

    uint256 private _userIdCounter = 1; 
    
    mapping(address => Users[]) public users;
    mapping(uint256 => address) public streamIdToAddress;
    mapping(uint256 => uint256) public streamIdToIndex;

    struct Users {
        uint256 idUsers;
        string name;
        uint256 balance;
        address sender; 
        bool active;
        uint256 streamId; 
    }

    constructor () {
        _owner = msg.sender;
    }

    modifier onlyOwner(){
        require(msg.sender == _owner, "Bukan Owner");
        _;
    }

    function createUsers(
        string memory name,
        uint256 balance,
        address sender,
        bool active
    ) 
    external  
    onlyOwner
    payable 
    returns (uint256 streamId) 
    {
        uint256 index = users[sender].length;
        streamId = index + 1;
        uint256 userId = _userIdCounter;
        _userIdCounter++;

        users[sender].push(
            Users({
                idUsers: userId,
                name: name,
                balance: balance,
                sender: sender,
                active: active,
                streamId: streamId
            })
        );

        streamIdToAddress[streamId] = sender;
        streamIdToIndex[streamId] = index;

        return streamId;
    }

    function getUsersLength(
        uint256 streamId
    ) 
    external 
    view 
    returns ( Users memory ) 
    {
        address sender = streamIdToAddress[streamId];
        uint256 index = streamIdToIndex[streamId];

        require(sender != address(0), "Stream ID tidak ditemukan");
        require(index < users[sender].length, "Index invalid");

        return users[sender][index];
    }

    function getOwner() external view returns (address) {
        return _owner;
    }
}

//0xf4ea49eaa04cdc2b4c45a0c4570fbca24a315c56
//0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2


<div class="flex gap-6 justify-center p-10 bg-[#03182a] overflow-x-auto">
  
  <!-- CARD -->
  <div class="w-56 bg-[#31126b] rounded-xl overflow-hidden text-white
              transform rotate-[-8deg] transition-all duration-300 shadow-xl
              hover:rotate-0 hover:scale-105 hover:shadow-[0_0_35px_rgba(0,255,255,0.7)]">
    <img src="https://via.placeholder.com/300x300" class="w-full">
    <div class="p-4">
      <h3 class="text-lg font-bold">Degen Ape #9244</h3>
      <p class="text-sm opacity-70">Degenerate Ape Academy</p>
      <div class="mt-2 bg-black/40 px-3 py-1 rounded-full w-fit text-sm">
        40 ◎
      </div>
    </div>
  </div>

  <!-- CARD 2 -->
  <div class="w-56 bg-[#31126b] rounded-xl overflow-hidden text-white
              transform rotate-[3deg] transition-all duration-300 shadow-xl
              hover:rotate-0 hover:scale-105 hover:shadow-[0_0_35px_rgba(0,255,255,0.7)]">
    <img src="https://via.placeholder.com/300x300" class="w-full">
    <div class="p-4">
      <h3 class="text-lg font-bold">Dope Apes #1400</h3>
      <p class="text-sm opacity-70">Dope Apes</p>
      <div class="mt-2 bg-black/40 px-3 py-1 rounded-full w-fit text-sm">
        1.44 ◎
      </div>
    </div>
  </div>

  <!-- CARD 3 -->
  <div class="w-56 bg-[#31126b] rounded-xl overflow-hidden text-white
              transform rotate-[10deg] transition-all duration-300 shadow-xl
              hover:rotate-0 hover:scale-105 hover:shadow-[0_0_35px_rgba(0,255,255,0.7)]">
    <img src="https://via.placeholder.com/300x300" class="w-full">
    <div class="p-4">
      <h3 class="text-lg font-bold">Aurorian #827</h3>
      <p class="text-sm opacity-70">Aurory</p>
      <div class="mt-2 bg-black/40 px-3 py-1 rounded-full w-fit text-sm">
        23 ◎
      </div>
    </div>
  </div>

</div>


https://base-sepolia.g.alchemy.com/v2/QcdKR1IT-vm0xIVZlf_vs
DKU55KCDAPNMW71INEDRJ9XJYA7SBTA26S
https://base-sepolia.g.alchemy.com/v2/QcdKR1IT-vm0xIVZlf_vs
