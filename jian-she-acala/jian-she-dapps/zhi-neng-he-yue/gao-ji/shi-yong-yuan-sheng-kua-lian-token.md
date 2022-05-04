# 使用原生&跨链Token

部署在Acala EVM中的智能合约Dapp可以直接使用原生和跨链资产，如DOT、ACA、aUSD、renBTC等。部署在EVM中的ERC-20Token也在Runtime层级可用、在DeX中列出，或者（经管理部门批准）作为收费Token使用。在[这里](../../../../le-jie-acala/acala-evm+/acala-evm+/ke-zu-he-de-defi-zhan.md)阅读更多信息。

## ERC20 合约地址

| Token符号  | ER20地址                                       |   |
| -------- | -------------------------------------------- | - |
| ACA      | `0x0000000000000000000000000000000001000000` |   |
| AUSD     | `0x0000000000000000000000000000000001000001` |   |
| DOT      | `0x0000000000000000000000000000000001000002` |   |
| LDOT     | `0x0000000000000000000000000000000001000003` |   |
| XBTC     | `0x0000000000000000000000000000000001000004` |   |
| RENBTC   | `0x0000000000000000000000000000000001000005` |   |
| POLKABTC | `0x0000000000000000000000000000000001000006` |   |
| PLM      | `0x0000000000000000000000000000000001000007` |   |
| PHA      | `0x0000000000000000000000000000000001000008` |   |
| HDT      | `0x0000000000000000000000000000000001000009` |   |
| KAR      | `0x0000000000000000000000000000000001000080` |   |
| KUSD     | `0x0000000000000000000000000000000001000081` |   |
| KSM      | `0x0000000000000000000000000000000001000082` |   |
| LKSM     | `0x0000000000000000000000000000000001000083` |   |
| SDN      | `0x0000000000000000000000000000000001000087` |   |
| Oracle   | `0x0000000000000000000000000000000000000801` |   |
| Schedule | `0x0000000000000000000000000000000000000802` |   |

## 合约方法

```javascript
// Returns the currencyId of the token.
function currencyId() public view returns (uint256);

// Returns the name of the token.
function name() public view returns (string memory);

// Returns the symbol of the token, usually a shorter version of the name.
function symbol() public view returns (string memory);

// Returns the number of decimals used to get its user representation.
function decimals() public view returns (uint8);

// Returns the amount of tokens in existence.
function totalSupply() public view returns (uint256);

// Returns the amount of tokens owned by `account`.
function balanceOf(address account) public view returns (uint256);

// Moves `amount` tokens from the caller's account to `recipient`.
// Returns a boolean value indicating whether the operation succeeded.
// Emits a {Transfer} event.
function transfer(address recipient, uint256 amount) public returns (bool);

// Returns the remaining number of tokens that `spender` will be allowed to spend on behalf of `owner` through {transferFrom}. 
// This is zero by default.
function allowance(address owner, address spender) public view returns (uint256);

// Sets `amount` as the allowance of `spender` over the caller's tokens.
// Returns a boolean value indicating whether the operation succeeded.
function approve(address spender, uint256 amount) public returns (bool);

// Moves `amount` tokens from `sender` to `recipient` using the allowance mechanism. `amount` is then deducted from the caller's allowance.
// Returns a boolean value indicating whether the operation succeeded.
function transferFrom(address sender, address recipient, uint256 amount) public returns (bool);

// Atomically increases the allowance granted to `spender` by the caller.
// This is an alternative to {approve} that can be used as a mitigation for problems described in {IERC20-approve}.
// Emits an {Approval} event indicating the updated allowance.
function increaseAllowance(address spender, uint256 addedValue) public returns (bool);

// Atomically decreases the allowance granted to `spender` by the caller.
// This is an alternative to {approve} that can be used as a mitigation for problems described in {IERC20-approve}.
// Emits an {Approval} event indicating the updated allowance.
function decreaseAllowance(address spender, uint256 subtractedValue) public returns (bool);
```

More details and source code [here](https://github.com/AcalaNetwork/predeploy-contracts#erc20-contracts).
