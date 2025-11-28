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
