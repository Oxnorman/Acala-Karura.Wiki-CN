# Runtime事件

## 与拍卖相关的

| 事件                   | 参数                                                                                                                                                                                                                       | 描述      | 模块             |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------- | -------------- |
| NewCollateralAuction | 1. `AuctionId` : new collateral auction id\</br> 2. `CurrencyId` : collateral type\</br> 3. `Balance` : collateral amount\</br> 4. `Balance` : target aUSD amount, when bid >= target, auction is in reverse stage\</br> | 创建抵押品拍卖 | AuctionManager |
| NewDebitAuction      | 1. `AuctionId` : auction id\</br> 2. `Balance` : initial avalible ACA amount \</br> 3. `Balance` : fixed aUSD amount, bid must >= it\</br>                                                                               | 创建债务拍卖  | AuctionManager |
| NewSurplusAuction    | 1. `AuctionId` : auction id\</br> 2. `Balance` : aUSD amount of surplus\</br>                                                                                                                                            | 创建盈余拍卖  | AuctionManager |
| CancelAuction        | 1. `AuctionId` : auction id\</br>                                                                                                                                                                                        | 取消拍卖    | AuctionManager |
| AuctionDealed        | 1. `AuctionId` : auction id\</br>                                                                                                                                                                                        | 拍卖成交    | AuctionManager |
| Bid                  | 1. `AuctionId` : auction id\</br> 2. `AccountId` : bidder address \</br> 3. `Balance` : bid price\</br>                                                                                                                  | 出价成功    | Auction        |

## DEX 相关的

| 事件                | 参数                                                                                                                                                                                                                                                                           | 描述                     | 模块  |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- | --- |
| AddLiquidity      | 1. `AccountId` : who add liquidity to pool\</br> 2. `CurrencyId` : specific liquidity pool of **other token** / aUSD pair\</br> 3. `Balance` : other token amount added\</br> 4. `Balance` : aUSD amount added\</br> 5. `Share` : increased share amount\</br>               | 添加流动性到特定池子             | Dex |
| WithdrawLiquidity | 1. `AccountId` : who withdraw liquidity from pool\</br> 2. `CurrencyId` : specific liquidity pool of **other token** / aUSD pair\</br> 3. `Balance` : other token amount withdrew \</br> 4. `Balance` : aUSD amount withdrew\</br> 5. `Share` : decreased share amount\</br> | 从特定池子提取流动性             | Dex |
| Swap              | 1. `AccountId` : exchanger\</br> 2. `CurrencyId` : the token type which exchanger sold to DEX \</br> 3. `Balance` : amount of sold token \</br> 4. `CurrencyId` : the token type which exchanger bought from DEX\</br> 5. `Balance` : amount of bought token\</br>           | 用token通过DEX兑换另外一种token | Dex |

## Homa协议相关的

| 事件                     | 参数                                                                                                                                                                                                          | 描述                        | 模块          |
| ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------- | ----------- |
| BondAndMint            | 1. `AccountId` : caller\</br> 2. `Balance` : DOT amount to bond by homa protocol \</br> 3. `Balance` : issued LDOT amount to caller\</br>                                                                   | 将DOT锁定到Homa协议中，然后发行流动性DOT | StakingPool |
| RedeemByUnbond         | 1. `AccountId` : caller\</br> 2. `Balance` : amount of LDOT to redeem\</br>                                                                                                                                 | 通过正常解绑来赎回 DOT             | StakingPool |
| RedeemByFreeUnbonded   | 1. `AccountId` : caller\</br> 2. `Balance` : fee in LDOT\</br> 3. `Balance` : LDOT amount to redeem\</br> 4. `Balance` : redeemed DOT amount\</br>                                                          | 通过Homa自由池来直接赎回 DOT        | StakingPool |
| RedeemByClaimUnbonding | 1. `AccountId` : caller\</br> 2. `EraIndex`: target era index to claim redeption\</br> 3. `Balance` : fee in LDOT\</br> 4. `Balance` : LDOT amount to redeem\</br> 5. `Balance` : redeemed DOT amount\</br> | 领取解绑DOT来赎回DOT             | StakingPool |

## CDP 相关的

| 事件                           | 参数                                                                                                                                                                                                                                                                                                                                                                                              | 描述                                      | 模块        |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------- | --------- |
| Authorization                | 1. `AccountId` : authorizer account\</br> 2. `AccountId` : the authorized account\</br> 3. `CurrencyId` : the authorized loan type\</br>                                                                                                                                                                                                                                                        | 一个账户授权另一个账户来操作其特定类型的借贷                  | Honzon    |
| UnAuthorization              | 1. `AccountId` : authorizer account\</br> 2. `AccountId` : the authorized account\</br> 3. `CurrencyId` : the authorized loan type\</br>                                                                                                                                                                                                                                                        | 授权人账户撤销授权账户对特定类型贷款的操作权                  | Honzon    |
| UnAuthorizationAll           | 1. `AccountId` : authorizer account\</br>                                                                                                                                                                                                                                                                                                                                                       | 撤销对所有贷款类型的其他账户的所有授权                     | Honzon    |
| LiquidateUnsafeCDP           | 1. `CurrencyId` : collateral token type\</br> 2. `AccountId` : owner of the liquidated CDP\</br> 3. `Balance` : the confiscated amount for liquidation\</br> 4. `Balance` : the bad debt amount(in aUSD) produced by the liquidated Cdp\</br>                                                                                                                                                   | 清算一个非安全的CDP                             | CdpEngine |
| SettleCDPInDebit             | 1. `CurrencyId` : collateral token type\</br> 2. `AccountId` : owner of the settled CDP\</br>                                                                                                                                                                                                                                                                                                   | 在紧急关停开启之后结算一个有债务的CDP                    | CdpEngine |
| UpdatePosition               | 1. `AccountId` : CDP's owner\</br> 2. `CurrencyId` : CDP's collateral type\</br> 3. `Amount` : collateral adjustment amount, positive means collateral increased, negative means collateral decreased\</br> 4. `DebitAmount` : debit adjustment amount, positive means CDP's debit increased and owner get more aUSD loan, negative means CDP's debit decreased and owner repay some debt\</br> | cdp 所有者操作他的贷款和抵押品                       | Loans     |
| ConfiscateCollateralAndDebit | 1. `AccountId` : CDP's owner\</br> 2. `CurrencyId` : CDP's collateral type\</br> 3. `Balance` : collateral amount to be confiscated \</br> 4. `DebitBalance` : debit balance to be confiscated \</br>                                                                                                                                                                                           | 系统操作中的CDP清除，如结算、清算等。                    | Loans     |
| TransferLoan                 | 1. `AccountId` : sender\</br> 2. `AccountId` : receiver\</br> 3. `CurrencyId` : collateral type\</br>                                                                                                                                                                                                                                                                                           | 发送者将他的全部特定抵押品CDP（包括所有抵押品金额和借贷金额）转移给收款人。 | Loans     |



## 紧急关停相关的

| 事件         | 参数                                                               | 描述     | 模块                |
| ---------- | ---------------------------------------------------------------- | ------ | ----------------- |
| Shutdown   | 1. `BlockNumber` : block number the emergency shutdown occurs    | 系统紧急关停 | EmergencyShutdown |
| OpenRefund | 1. `BlockNumber` : block number when refund operation is allowed | 退款操作开启 | EmergencyShutdown |
| Refund     | 1. `Balance` : aUSD amount used to refund                        | 退款成功   | EmergencyShutdown |

## 风险管理参数相关的 <a href="#risk-management-parameters-related" id="risk-management-parameters-related"></a>

| 事件                                 | 参数                                                                                                                         | 描述   | 模块          |
| ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------- | ---- | ----------- |
| UpdateStabilityFee                 | 1. `CurrencyId` : collateral type\</br> 2. `Option<Rate>` : extra stalibity fee rate                                       | 参数更新 | CdpTreasury |
| UpdateLiquidationRatio             | 1. `CurrencyId` : collateral type\</br> 2. `Option<Ratio>` : liquidation ratio                                             | 参数更新 | CdpTreasury |
| UpdateLiquidationPenalty           | 1. `CurrencyId` : collateral type\</br> 2. `Option<Rate>` : extra penalty rate when CDP liquidated                         | 参数更新 | CdpTreasury |
| UpdateRequiredCollateralRatio      | 1. `CurrencyId` : collateral type\</br> 2. `Option<Ratio>` : the limit of collateral ratio when owner manipulate           | 参数更新 | CdpTreasury |
| UpdateMaximumTotalDebitValue       | 1. `CurrencyId` : collateral type\</br> 2. `Balance` : aUSD cap issued by this type of collateral                          | 参数更新 | CdpTreasury |
| UpdateSurplusAuctionFixedSize      | 1. `Balance` : fixed aUSD amount to be sold in a surplus auction\</br>                                                     | 参数更新 | CdpTreasury |
| UpdateSurplusBufferSize            | 1. `Balance` : surplus pool buffer size, surplus auction is only created when surplus pool exceed it\</br>                 | 参数更新 | CdpTreasury |
| UpdateInitialAmountPerDebitAuction | 1. `Balance` : initial ACA amount to be sold in a debit auction\</br>                                                      | 参数更新 | CdpTreasury |
| UpdateDebitAuctionFixedSize        | 1. `Balance` : fixed aUSD amount to buy a debit auction\</br>                                                              | 参数更新 | CdpTreasury |
| UpdateCollateralAuctionMaximumSize | 1. `CurrencyId` : collateral type\</br> 2. `Balance` : max collateral amount to be sold when create new collateral auction | 参数更新 | CdpTreasury |

