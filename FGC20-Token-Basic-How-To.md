# FGC20 Token

## About FGC20

FGC20 is the implementation of a standard API for tokens within smart contracts on FantasyGold，basically it is the same as [ERC20](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-20.md).
<br>
Methods and Events：

```
function name() constant returns (string name)
function symbol() constant returns (string symbol)
function decimals() constant returns (uint8 decimals)
function totalSupply() constant returns (uint256 totalSupply)
function balanceOf(address _owner) constant returns (uint256 balance)
function transfer(address _to, uint256 _value) returns (bool success)
function transferFrom(address _from, address _to, uint256 _value) returns (bool success)
function approve(address _spender, uint256 _value) returns (bool success)
function allowance(address _owner, address _spender) constant returns (uint256 remaining)
event Transfer(address indexed _from, address indexed _to, uint256 _value)
event Approval(address indexed _owner, address indexed _spender, uint256 _value)
```

## Implementation

Token example：[FGC20Token](https://github.com/fantasygold/FGC20Token), you can use this code to publish your token on the FantasyGold blockchain.

In [FGC20Token.sol](https://github.com/fantasygold/FGC20Token/blob/master/FGC20Token.sol), change `name`、`symbol` and `totalSupply` to your own preference.

![](https://i.imgur.com/D8SyAY6.png)


## Deployment

### Install the wallet

Download the latest FantasyGold Core wallet from [https://github.com/FantasyGold/FantasyGold-Core/releases](https://github.com/FantasyGold/FantasyGold-Core/releases).

Once you have the wallet installed and synced create a new FGC address and send some FGC to the address to cover the gas fee.
<br>
Click `Request payment` to get your receive address.

![](https://i.imgur.com/ZtxDxBX.png)

### Compile the code

Open [https://ethereum.github.io/browser-solidity/](https://ethereum.github.io/browser-solidity/) in your browser. Direct links to both solidity and the example code are also located in the Smart Contacts -> Create section of the wallet. 

Click the “+” button on the top-right side，create new files `SafeMath.sol` and `FGC20Token.sol`, copy & paste your smart contract code in those two files.


![](https://i.imgur.com/0oAPt3r.png)
<br>
Click “Compile” on the left side, and then "Compilation Details" and copy the BYTECODE. (The long string of numbers following "objects")

![](https://i.imgur.com/uFelsqk.png)


### Create contract

Open FantasyGold Core wallet, go to “Smart Contract” -> “Create”, paste the BYTECODE.

![](https://i.imgur.com/JdwAFZU.png)
<br>
Now at the bottom select the `SenderAddress` as the address you already funded with FGC in the steps above and then click the “Create Contract” button at the bottom right and then save the `SenderAddress` and `ContractAddress` for when your ready to add your token to the wallet. Make sure any FGC that was sent to the newly funded address is fully confirmed BEFORE you click “Create Contract”

![](https://i.imgur.com/g1ozw1K.png)
<br>
Wait until the transaction gets confirmed and the token is mined on the chain. 

## Wallet Usage

### Adding Tokens

In FantasyGold Core wallet, go to “FGC Token” page and click “Add Token” button, input your `Contact Address`, the "Token Name", "Token Symbol" and the "Decimals" should then auto populate their fields, if not check to see the Token transaction is fully confirmed. Then choose `SenderAddress` as your `Token Address` and click the “Confirm” button. 

![](https://i.imgur.com/zmcl0zs.png)

If you cannot find the `SenderAddress` in the `Token Address` combobox, please send some fantasygold coins to the `SenderAddress` and try again.

### Receive and send tokens

In “FGC Token” page, click to choose your token，the you can click the “Send” or “Receive” button below to receive or send tokens.

![](https://i.imgur.com/AKR4M3H.png)
<br>
![](https://i.imgur.com/o2PeDn6.png)


## More to know

* A small amount of FGC is needed to pay for the token sending gas fee, please ensure you have enough FGCs in the token binding address.




