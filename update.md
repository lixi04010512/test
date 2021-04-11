pragma solidity ^0.6.0;

contract UserManager {
    address payable public owner;
    
    mapping(uint8 => string) accounts;    //id -> passwd
    mapping(uint8 => address) ips;       //IP address
    mapping(address=> bool) isExist;
    
    event Login(uint8 id, uint time);
    event Register();
    event SetPassword();
    
    constructor () public {
        owner = msg.sender;
    }
    
    function login(uint8 id, string memory passwd) public returns (bool) {
         require(equal(accounts[id],passwd),"...");
         return true;
    }
    
      function register(uint8 id, string memory passwd) public returns (bool) {
        require(!isExist[msg.sender],"");
         require(equal(accounts[id],""));
         accounts[id] =passwd;
         isExist[msg.sender]=true;
    }
    
    function equal(string memory a,string memory b) public returns(bool){
        require(keccak256(abi.encodePacked(a)) == keccak256(abi.encodePacked(b)));
    }
    
    function getIP(uint8 id) public view returns (address) {
        require(ips[id] != address(0));
        return ips[id];
    }
    
    function setPassword(uint8 id,string memory passwd) public returns (bool) {
        require(!isExist[msg.sender],"");
         require(equal(accounts[id],""));
         accounts[id] =passwd;
         isExist[msg.sender]=true;
    }
  }