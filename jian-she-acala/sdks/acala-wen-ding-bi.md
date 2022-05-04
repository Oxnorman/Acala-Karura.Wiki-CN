# Acala 稳定币

通过Javascript来与Acala和Karura互动，你可以使用 `@polkadot/api` 和`@acala-network/api`. 你可以在[这里](https://polkadot.js.org/docs/api/)了解更多关于 `@polkadot/api` ([https://polkadot.js.org/docs/api](https://polkadot.js.org/docs/api)).我们也提供 [稳定币 SDK](https://github.com/AcalaNetwork/acala.js/tree/master/packages/sdk-loan) ，它提供了更多关于稳定币的自动功能

## Karura稳定币的源代码 <a href="#source-code-of-karura-stablecoin" id="source-code-of-karura-stablecoin"></a>

​[https://github.com/AcalaNetwork/Acala/tree/master/modules/honzon](https://github.com/AcalaNetwork/Acala/tree/master/modules/honzon)​

## 只读功能 (状态查询) <a href="#read-only-functions-state-queries" id="read-only-functions-state-queries"></a>

这些功能只能从链上读取信息，因而不需要用私钥签名交易。关于更多状态查询信息请点击： [状态查询文档](https://polkadot.js.org/docs/api/start/api.query)​

### 针对特定账户的给定抵押物类型获取铸币池 <a href="#get-vault-for-specific-account-for-given-collateral-type" id="get-vault-for-specific-account-for-given-collateral-type"></a>

针对特定的抵押品类型和账户进行借款，返回抵押品的数量以及以铸造的稳定币数量&#x20;

> 请注意⚠借款只反映铸造的aUSD数量。但债务会更高一些，因为它包含了累积的利息。为了计算需要偿还金额，怒需要使用 `debitExchangeRate` 参数 (如何取得 `debitExchangeRate` 参数的方法列举如下).

```typescript
positions(currencyId: CurrencyId, accountId: AccountId):
    Promise<{collateral: number, debit: number}>
```

**定义**

| 名称   | 类型         | 内容               |
| ---- | ---------- | ---------------- |
| 货币ID | CurrencyId | 抵押品的货币ID         |
| 账户ID | AccountId  | 创建铸币池的账户， 以字符串发送 |

**示例：**

```typescript
    const result = await api.query.loans.positions(
        { TOKEN: "KSM" },
        "<ACCOUNT>"
    );
  console.log(result.toHuman());
```

#### 全代码摘要: <a href="#full-code-snippet" id="full-code-snippet"></a>

​[loan-examples/get-positions.js](https://github.com/AcalaNetwork/acala-js-example/blob/master/src/loan-examples/get-positions.ts)​

### 按照抵押品类型，获取抵押品的数量和借款的aUSD <a href="#get-total-amount-of-collateral-and-borrowed-kusd-for-collateral-type" id="get-total-amount-of-collateral-and-borrowed-kusd-for-collateral-type"></a>

返回特定抵押品种类的`抵押品`总数量以及借的aUSD的数量&#x20;

```typescript
totalPositions(currencyId: CurrencyId):
    Promise<{collateral: number, debit: number}>
```

**Arguments**

| 名称   | 类型         | 内容       |
| ---- | ---------- | -------- |
| 货币ID | CurrencyId | 抵押品的货币ID |

**示例：**

```typescript
    const result = await api.query.loans.positions(
        { TOKEN: "KSM" },
        "<ACCOUNT>"
    );
  console.log(result.toHuman());
```

#### 全代码摘要: <a href="#full-code-snippet-1" id="full-code-snippet-1"></a>

​[loan-examples/total-positions.ts](https://github.com/AcalaNetwork/acala-js-example/blob/master/src/loan-examples/total-positions.ts)​

### 对给定的抵押品类型获取风险系数 <a href="#get-risk-parameters-for-given-collateral-type." id="get-risk-parameters-for-given-collateral-type."></a>

每一种被Karura接受的抵押品类型都有不同的风险系数。这些系数的数值由Karura的治理进行控制**;**

```typescript
collateralParams(currencyId: CurrencyId):
    Promise<{
    maximumTotalDebitValue: number,
    interestRatePerSec: number, 
    liquidationRatio: number,
    liquidationPenalty: number,
    requiredCollateralRatio: number,

    }>
```

#### **定义**

| 名称   | 类型         | 内容       |
| ---- | ---------- | -------- |
| 货币ID | CurrencyId | 抵押品的货币ID |

#### 返回值

| 名称                      | 类型      | 含义                                                            |
| ----------------------- | ------- | ------------------------------------------------------------- |
| maximumTotalDebitValue  | Number  |  一个铸币池可能借出的最大aUSD数量                                           |
| interestRatePerSec      | Percent | 借出的aUSD在每个区块需要偿还的百分比，这个数量应添加到`globalInterestRatePerSec` 来计算债务 |
| liquidationRatio        | Percent | 抵押率（抵押来的价值/债务价值）达到铸币池需要被清算的临界值                                |
| liquidationPenalty      | Percent | 如果铸币池进行清算，铸币池需要收取的罚金                                          |
| requiredCollateralRatio | Percent | 用户借贷aUSD的最小抵押率                                                |

示例：

```
    const result = await api.query.cdpEngine.collateralParams({ 
      TOKEN: "KSM" 
    });
    console.log(result.toHuman());
```

#### 全节点摘要: <a href="#full-code-snippet-2" id="full-code-snippet-2"></a>

​[loan-examples/collateral-params.ts](https://github.com/AcalaNetwork/acala-js-example/blob/master/src/loan-examples/collateral-params.ts)​

### 给定抵押品类型，获取债务汇率 <a href="#get-debt-exchange-rate-for-given-collateral-type" id="get-debt-exchange-rate-for-given-collateral-type"></a>

该参数用于计算债务。铸造的aUSD应当乘以该汇率。利息的累计基于区块高度，所以应当每隔一定数量的区块就提取该参数。

```typescript
debitExchangeRate(currencyId: CurrencyId):
    Promise<number}>
```

#### 定义

| 名称   | 类型         | 内容       |
| ---- | ---------- | -------- |
| 货币ID | CurrencyId | 抵押品的货币ID |

示例:

```
  const result = await api.query.cdpEngine.debitExchangeRate.at(
      '<BLOCK_HASH'
      { TOKEN: "KSM" }
  );
  console.log(result.toHuman());
```

#### 全代码摘要: <a href="#full-code-snippet-3" id="full-code-snippet-3"></a>

​[loan-examples/debit-exchange-rate.ts](https://github.com/AcalaNetwork/acala-js-example/blob/master/src/loan-examples/debit-exchange-rate.ts)​

## 状态改变功能 <a href="#state-changing-functions" id="state-changing-functions"></a>

这些交易将数据写到链上，并且需要私钥对其签名。为了测试代码摘要，请确保你有 `SEED_PHRASE` 环境变量，该变量已经定义在你的 `.env` 文件中。

### 创建和管理铸币池 <a href="#create-and-manage-the-vault" id="create-and-manage-the-vault"></a>

所有的操作：创建铸币池，添加/删除抵押品，借贷，偿还aUSD 都可以通过单一方法实现： `honzon.adjustLoan`

```typescript
adjustLoan(currency_id: CurrencyId, collateral_adjustment: Number, debit_adjustment: Number): Extrinsic
```

****

**定义**

| 名称                     | 类型            | 内容                                 |
| ---------------------- | ------------- | ---------------------------------- |
| currencyId             | CurrencyId    | 抵押品的货币ID                           |
| collateral\_adjustment | Signed Amount | 正数表示将抵押品货币存入铸币池，负数表示将抵押品从铸币池中提取    |
| debit\_adjustment      | Signed Amount | 正数表示铸造一定数量的稳定币给调用者，负数表示调用者还给铸币池稳定币 |

示例：

```typescript
  const currencyId = { TOKEN: "KSM" };
  const collateralAdjustment = <DESIRED_ADJUSTMENT>;
  const debitAdjustment = <DESIRED_ADJUSTMENT>;

  const extrinsic = api.tx.honzon.adjustLoan(
    currencyId,
    collateralAdjustment,
    debitAdjustment
  );
  const hash = await extrinsic.signAndSend(signer);
  console.log('hash', hash.toHuman());
```

> 请注意⚠供应量的数值必须与KAR的小数点位保持一致，入这个例子所示

#### 全代码摘要: <a href="#full-code-snippet-4" id="full-code-snippet-4"></a>

​[loan-examples/adjustLoan.ts](https://github.com/AcalaNetwork/acala-js-example/blob/master/src/loan-examples/adjustLoan.ts)​

### 获得转移借款的权限 <a href="#grants-permission-for-transferring-loan" id="grants-permission-for-transferring-loan"></a>

为将调用者的借款转移到另外一个账户设置权限。

```typescript
authorize(curencyId: CurrencyId, to: AccountId): Extrinsic
```

返回 `Extrinsic` 类型，该数值要求有私钥签名。

**定义**

| 名称         | 类型         | 内容            |
| ---------- | ---------- | ------------- |
| currencyId | CurrencyId | 抵押品的货币ID      |
| to         | AccountId  | 为转移借款到此账户设置权限 |

**示例**:

```typescript
  const accountId = "<ACCOUNT_ID>";
  const extrinsic = api.tx.honzon.authorize(
    { TOKEN: "KSM" }, 
    accountId
  );
  const hash = await extrinsic.signAndSend(signer);
  console.log("hash", hash.toHuman());
```

#### 全代码摘要:

​[loan-examples/authorize.ts](https://github.com/AcalaNetwork/acala-js-example/blob/master/src/loan-examples/authorize.ts)​

### 取消转移借款的权限 <a href="#removes-permission-for-transferring-loan" id="removes-permission-for-transferring-loan"></a>

取消将调用者借款转移到其他所有账户的权限，所有的抵押品类型都被取消。该方法用于去解决之间已授权限。

```
unauthorizeAll(): Extrinsic
```

返回 `Extrinsic` 的类型，该类型应当有私钥签名。

**示例**:

```typescript
  const extrinsic = api.tx.honzon.unauthorizeAll();
  const hash = await extrinsic.signAndSend(signer);
  console.log("hash", hash.toHuman());
```

### 将铸币池转移到其他账户 <a href="#transfering-vault-to-another-account" id="transfering-vault-to-another-account"></a>

如果有许可（该账户之前已经授权），将该账户的铸币池转移到调用者账户。

```
transferLoanFrom(currency_id, from): Extrinsic
```

返回 `Extrinsic` 的类型，该类型应当有私钥签名。

**定义**

| 名称         | 类型         | 内容                |
| ---------- | ---------- | ----------------- |
| currencyId | CurrencyId | 抵押品的货币ID          |
| from       | AccountId  | 从此账户中将抵押品转移到调用者账户 |

**示例**:

```typescript
    const fromAccountId = "<ACCOUNT_ID>";
    const extrinsic = api.tx.honzon.transferLoanFrom(
      { TOKEN: "KSM" },
      fromAccountId
    );
    const hash = await extrinsic.signAndSend(signer);
    console.log("hash", hash.toHuman());
```

### 通过在DEX中兑换抵押品来关闭调用者铸币池 <a href="#closing-callers-vault-by-swapping-collateral-in-dex" id="closing-callers-vault-by-swapping-collateral-in-dex"></a>

通过 `adjustLoan`即可实现， 但这里有一条只适用于安全的铸币池（也就是抵押率高于清算率）和债务金额为正的捷径。这种方法通过在Karura DEX上出售足够数量的抵押品来关闭调用者的铸币池。

```typescript
closeLoanHasDebitByDex(
    currency_id: CurrencyId, 
    max_collateral_amount: number, 
    maybe_path?: CurrencyId[]
): Extrinsic
```

返回 `Extrinsic` 的类型，该类型应当有私钥签名。

**定义：**

| 名称                      | 类型            | 内容                          |
| ----------------------- | ------------- | --------------------------- |
| currencyId              | CurrencyId    | 抵押品的货币ID                    |
| max\_collateral\_amount | number        | 允许在DeX兑换额最大抵押品数量，用以偿还铸币池的借贷 |
| maybe\_path             | CurrencyId\[] | 可用于在DeX中，为获得aUSD而兑换抵押品的兑换路径 |

**示例**:

```typescript
    const extrinsic = api.tx.honzon.closeLoanHasDebitByDex(
      { TOKEN: "KSM" },
      // large number, allows swapping almost any amount
      1 * 10 ** 30,
      [{ TOKEN: "KSM" }, { TOKEN: "KUSD" }]
    );
    const hash = await extrinsic.signAndSend(signer);
    console.log("hash", hash.toHuman());
```

#### 全节点摘要: <a href="#full-code-snippet-6" id="full-code-snippet-6"></a>

​[loan-examples/close-vault-with-dex.ts](https://github.com/AcalaNetwork/acala-js-example/blob/master/src/loan-examples/close-vault-with-dex.ts)​
