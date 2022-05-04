# 使用链上调度器

你可以使用链上调度器合约来安排重复性的调用给定的智能合约。在[这里](../../../../../le-jie-acala/acala-evm+/acala-evm+/lian-shang-tiao-du-qi.md)阅读更多关于链上自动调度器的使用案例。&#x20;

合约源代码在[这里](https://github.com/AcalaNetwork/predeploy-contracts/blob/master/contracts/schedule/Schedule.sol)。&#x20;

注意：`min_delay`是当前区块之后，计划调用程序被调用之前，这之间的最小区块数。比如 Pass 0意味着它将被安排在下一个区块进行调用。在区块10上调用`min_delay=5`的`scheduleCall`，将会安排在区块`10+1+5=16`上实现调用。如果区块已满或有太多的其他计划任务，计划的调用可以推迟到以后的区块，直到区块中有足够的剩余空间。&#x20;

## 合同地址&#x20;

ScheduleCall合同地址：`0x0000000000000000000000000000000000000808`

## `合约方法`

```javascript
// Schedule call the contract.
// Returns the task_address(block_number, index).
function scheduleCall(
  address contract_address, // The contract address to be called in future.
  uint256 value, // How much native token to send alone with the call.
  uint256 gas_limit, // The gas limit for the call. Corresponding fee will be reserved upfront and refunded after call.
  uint256 storage_limit, // The storage limit for the call. Corresponding fee will be reserved upfront and refunded after call.
  uint256 min_delay, // Minimum number of blocks before the scheduled call will be called.
  bytes memory input_data // The input data to the call.
)
public
returns (uint256, uint256); // Returns a task id that can be used to cancel or reschedule call.
```

## 示例

[这里有](https://github.com/AcalaNetwork/evm-examples/tree/master/scheduler) 一个使用调用器，进行周期性支付的合约。

## 指南

请按照本指南在Acala EVM上来编写和部署一个基本的自动订阅合约。

