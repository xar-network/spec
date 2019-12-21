
## auction

#### type MsgPlaceBid

```go
type MsgPlaceBid struct {
	AuctionID ID             `json:"auction_id" yaml:"auction_id"`
	Bidder    sdk.AccAddress `json:"bidder" yaml:"bidder"`
	Bid       sdk.Coin       `json:"bid" yaml:"bid"`
	Lot       sdk.Coin       `json:"lot" yaml:"lot"`
}
```

MsgPlaceBid is the message type used to place a bid on any type of auction.

## coinswap

#### type MsgAddLiquidity

```go
type MsgAddLiquidity struct {
	Deposit       sdk.Coin       `json:"deposit"`        // coin to be deposited as liquidity with an upper bound for its amount
	DepositAmount sdk.Int        `json:"deposit_amount"` // exact amount of native asset being add to the liquidity pool
	MinReward     sdk.Int        `json:"min_reward"`     // lower bound UNI sender is willing to accept for deposited coins
	Deadline      time.Time      `json:"deadline"`
	Sender        sdk.AccAddress `json:"sender"`
}
```

MsgAddLiquidity - struct for adding liquidity to a reserve pool

#### type MsgRemoveLiquidity

```go
type MsgRemoveLiquidity struct {
	Withdraw       sdk.Coin       `json:"withdraw"`        // coin to be withdrawn with a lower bound for its amount
	WithdrawAmount sdk.Int        `json:"withdraw_amount"` // amount of UNI to be burned to withdraw liquidity from a reserve pool
	MinNative      sdk.Int        `json:"min_native"`      // minimum amount of the native asset the sender is willing to accept
	Deadline       time.Time      `json:"deadline"`
	Sender         sdk.AccAddress `json:"sender"`
}
```

MsgRemoveLiquidity - struct for removing liquidity from a reserve pool

#### type MsgRemoveLiquidity

```go
type MsgRemoveLiquidity struct {
	Withdraw       sdk.Coin       `json:"withdraw"`        // coin to be withdrawn with a lower bound for its amount
	WithdrawAmount sdk.Int        `json:"withdraw_amount"` // amount of UNI to be burned to withdraw liquidity from a reserve pool
	MinNative      sdk.Int        `json:"min_native"`      // minimum amount of the native asset the sender is willing to accept
	Deadline       time.Time      `json:"deadline"`
	Sender         sdk.AccAddress `json:"sender"`
}
```

MsgRemoveLiquidity - struct for removing liquidity from a reserve pool

#### type MsgTransactionOrder

```go
type MsgTransactionOrder struct {
	Input      sdk.Coin       `json:"input"`
	Output     sdk.Coin       `json:"output"`
	Deadline   time.Time      `json:"deadline"`
	Sender     sdk.AccAddress `json:"sender"`
	Recipient  sdk.AccAddress `json:"recipient"`
	IsBuyOrder bool           `json:"is_buy_order"`
}
```

## csdt

#### type MsgCreateOrModifyCSDT

```go
type MsgCreateOrModifyCSDT struct {
	Sender           sdk.AccAddress `json:"sender" yaml:"sender"`
	CollateralDenom  string         `json:"collateral_denom" yaml:"collateral_denom"`
	CollateralChange sdk.Int        `json:"collateral_change" yaml:"collateral_change"`
	DebtChange       sdk.Int        `json:"debt_change" yaml:"debt_change"`
}
```

MsgCreateOrModifyCSDT creates, adds/removes collateral/stable coin from a csdt
TODO Make this more user friendly - maybe split into four functions.

#### type MsgDepositCollateral

```go
type MsgDepositCollateral struct {
	Sender           sdk.AccAddress `json:"sender" yaml:"sender"`
	CollateralDenom  string         `json:"collateral_denom" yaml:"collateral_denom"`
	CollateralChange sdk.Int        `json:"collateral_change" yaml:"collateral_change"`
}
```

MsgDepositCollateral adds collateral to CSDT.

#### type MsgSettleDebt

```go
type MsgSettleDebt struct {
	Sender          sdk.AccAddress `json:"sender" yaml:"sender"`
	CollateralDenom string         `json:"collateral_denom" yaml:"collateral_denom"`
	DebtDenom       string         `json:"debt_denom" yaml:"debt_denom"`
	DebtChange      sdk.Int        `json:"debt_change" yaml:"debt_change"`
}
```

MsgSettleDebt returns debt to CSDT.

#### type MsgWithdrawCollateral

```go
type MsgWithdrawCollateral struct {
	Sender           sdk.AccAddress `json:"sender" yaml:"sender"`
	CollateralDenom  string         `json:"collateral_denom" yaml:"collateral_denom"`
	CollateralChange sdk.Int        `json:"collateral_change" yaml:"collateral_change"`
}
```

MsgWithdrawCollateral removes collateral to CSDT.

#### type MsgWithdrawDebt

```go
type MsgWithdrawDebt struct {
	Sender          sdk.AccAddress `json:"sender" yaml:"sender"`
	CollateralDenom string         `json:"collateral_denom" yaml:"collateral_denom"`
	DebtDenom       string         `json:"debt_denom" yaml:"debt_denom"`
	DebtChange      sdk.Int        `json:"debt_change" yaml:"debt_change"`
}
```

MsgWithdrawDebt withdraws debt from CSDT.

## denominations

#### type MsgBurnCoins

```go
type MsgBurnCoins struct {
	Amount sdk.Int        `json:"amount" yaml:"amount"`
	Symbol string         `json:"symbol" yaml:"symbol"`
	Owner  sdk.AccAddress `json:"owner" yaml:"owner"`
}
```

MsgBurnCoins defines the BurnCoins message

#### type MsgFreezeCoins

```go
type MsgFreezeCoins struct {
	Amount  sdk.Int        `json:"amount" yaml:"amount"`
	Symbol  string         `json:"symbol" yaml:"symbol"`
	Owner   sdk.AccAddress `json:"owner" yaml:"owner"`
	Address sdk.AccAddress `json:"address" yaml:"address"`
}
```

MsgFreezeCoins defines the FreezeCoins message

#### type MsgIssueToken

```go
type MsgIssueToken struct {
	SourceAddress  sdk.AccAddress `json:"source_address" yaml:"source_address"`
	Owner          sdk.AccAddress `json:"owner" yaml:"owner"`
	Name           string         `json:"name" yaml:"name"`
	Symbol         string         `json:"symbol" yaml:"symbol"`
	OriginalSymbol string         `json:"original_symbol" yaml:"original_symbol"`
	MaxSupply      sdk.Int        `json:"max_supply" yaml:"max_supply"`
	Mintable       bool           `json:"mintable" yaml:"mintable"`
}
```

MsgIssueToken defines a IssueToken message

#### type MsgMintCoins

```go
type MsgMintCoins struct {
	Amount sdk.Int        `json:"amount" yaml:"amount"`
	Symbol string         `json:"symbol" yaml:"symbol"`
	Owner  sdk.AccAddress `json:"owner" yaml:"owner"`
}
```

MsgMintCoins defines the MintCoins message

#### type MsgUnfreezeCoins

```go
type MsgUnfreezeCoins struct {
	Amount  sdk.Int        `json:"amount" yaml:"amount"`
	Symbol  string         `json:"symbol" yaml:"symbol"`
	Owner   sdk.AccAddress `json:"owner" yaml:"owner"`
	Address sdk.AccAddress `json:"address" yaml:"address"`
}
```

MsgUnfreezeCoins defines the UnfreezeCoins message

## issue

#### type MsgIssue

```go
type MsgIssue struct {
	FromAddress  sdk.AccAddress `json:"from_address" yaml:"from_address"`
	*IssueParams `json:"params" yaml:"params"`
}
```

MsgIssue to allow a registered issuer to issue new coins.

#### type MsgIssueApprove

```go
type MsgIssueApprove struct {
	IssueId     string         `json:"issue_id" yaml:"issue_id"`
	FromAddress sdk.AccAddress `json:"from_address" yaml:"from_address"`
	ToAddress   sdk.AccAddress `json:"to_address" yaml:"to_address"`
	Amount      sdk.Int        `json:"amount" yaml:"amount"`
}
```

MsgIssueApprove to allow a registered owner

#### type MsgIssueBurnFrom

```go
type MsgIssueBurnFrom struct {
	IssueId     string         `json:"issue_id" yaml:"issue_id"`
	FromAddress sdk.AccAddress `json:"from_address" yaml:"from_address"`
	ToAddress   sdk.AccAddress `json:"to_address" yaml:"to_address"`
	Amount      sdk.Int        `json:"amount" yaml:"amount"`
}
```

MsgIssueBurnFrom to allow a registered owner

#### type MsgIssueBurnHolder

```go
type MsgIssueBurnHolder struct {
	IssueId     string         `json:"issue_id" yaml:"issue_id"`
	FromAddress sdk.AccAddress `json:"from_address" yaml:"from_address"`
	Amount      sdk.Int        `json:"amount" yaml:"amount"`
}
```

MsgIssueBurnHolder to allow a registered owner

#### type MsgIssueBurnOwner

```go
type MsgIssueBurnOwner struct {
	IssueId     string         `json:"issue_id" yaml:"issue_id"`
	FromAddress sdk.AccAddress `json:"from_address" yaml:"from_address"`
	Amount      sdk.Int        `json:"amount" yaml:"amount"`
}
```

MsgIssueBurnOwner to allow a registered owner

#### type MsgIssueDecreaseApproval

```go
type MsgIssueDecreaseApproval struct {
	IssueId     string         `json:"issue_id" yaml:"issue_id"`
	FromAddress sdk.AccAddress `json:"from_address" yaml:"from_address"`
	ToAddress   sdk.AccAddress `json:"to_address" yaml:"to_address"`
	Amount      sdk.Int        `json:"amount" yaml:"amount"`
}
```

MsgIssueDecreaseApproval to allow a registered owner

#### type MsgIssueDescription

```go
type MsgIssueDescription struct {
	IssueId     string         `json:"issue_id" yaml:"issue_id"`
	FromAddress sdk.AccAddress `json:"from_address" yaml:"from_address"`
	Description []byte         `json:"description" yaml:"description"`
}
```

MsgIssueDescription to allow a registered owner to issue new coins.

#### type MsgIssueDisableFeature

```go
type MsgIssueDisableFeature struct {
	IssueId     string         `json:"issue_id" yaml:"issue_id"`
	FromAddress sdk.AccAddress `json:"from_address" yaml:"from_address"`
	Feature     string         `json:"feature" yaml:"feature"`
}
```

MsgIssueDisableFeature to allow a registered owner

#### type MsgIssueFreeze

```go
type MsgIssueFreeze struct {
	IssueId     string         `json:"issue_id" yaml:"issue_id"`
	FromAddress sdk.AccAddress `json:"from_address" yaml:"from_address"`
	ToAddress   sdk.AccAddress `json:"to_address" yaml:"to_address"`
	FreezeType  string         `json:"freeze_type" yaml:"freeze_type"`
}
```

MsgIssueFreeze to allow a registered owner

#### type MsgIssueIncreaseApproval

```go
type MsgIssueIncreaseApproval struct {
	IssueId     string         `json:"issue_id" yaml:"issue_id"`
	FromAddress sdk.AccAddress `json:"from_address" yaml:"from_address"`
	ToAddress   sdk.AccAddress `json:"to_address" yaml:"to_address"`
	Amount      sdk.Int        `json:"amount" yaml:"amount"`
}
```

MsgIssueIncreaseApproval to allow a registered owner

#### type MsgIssueMint

```go
type MsgIssueMint struct {
	IssueId     string         `json:"issue_id" yaml:"issue_id"`
	FromAddress sdk.AccAddress `json:"from_address" yaml:"from_address"`
	ToAddress   sdk.AccAddress `json:"to_address" yaml:"to_address"`
	Amount      sdk.Int        `json:"amount" yaml:"amount"`
}
```

MsgIssueMint to allow a registered issuer to issue new coins.

#### type MsgIssueSendFrom

```go
type MsgIssueSendFrom struct {
	IssueId     string         `json:"issue_id" yaml:"issue_id"`
	FromAddress sdk.AccAddress `json:"from_address" yaml:"from_address"`
	From        sdk.AccAddress `json:"from" yaml:"from"`
	ToAddress   sdk.AccAddress `json:"to_address" yaml:"to_address"`
	Amount      sdk.Int        `json:"amount" yaml:"amount"`
}
```

MsgIssueSendFrom to allow a registered owner

#### type MsgIssueTransferOwnership

```go
type MsgIssueTransferOwnership struct {
	IssueId     string         `json:"issue_id" yaml:"issue_id"`
	FromAddress sdk.AccAddress `json:"from_address" yaml:"from_address"`
	ToAddress   sdk.AccAddress `json:"to_address" yaml:"to_address"`
}
```

MsgIssueTransferOwnership to allow a registered owner to issue new coins.

#### type MsgIssueUnFreeze

```go
type MsgIssueUnFreeze struct {
	IssueId     string         `json:"issue_id" yaml:"issue_id"`
	FromAddress sdk.AccAddress `json:"from_address" yaml:"from_address"`
	ToAddress   sdk.AccAddress `json:"to_address" yaml:"to_address"`
	FreezeType  string         `json:"freeze_type" yaml:"freeze_type"`
}
```

MsgIssueUnFreeze to allow a registered owner

## liquidator

#### type MsgSeizeAndStartCollateralAuction

```go
type MsgSeizeAndStartCollateralAuction struct {
	Sender          sdk.AccAddress `json:"sender" yaml:"sender"`
	CsdtOwner       sdk.AccAddress `json:"owner" yaml:"owner"`
	CollateralDenom string         `json:"collateral_denom" yaml:"collateral_denom"`
}
```

#### type MsgStartDebtAuction

```go
type MsgStartDebtAuction struct {
	Sender sdk.AccAddress `json:"sender" yaml:"sender"`
}
```

#### type SeizeAndStartCollateralAuctionRequest

```go
type SeizeAndStartCollateralAuctionRequest struct {
	BaseReq         rest.BaseReq   `json:"base_req"`
	Sender          sdk.AccAddress `json:"sender"`
	CdpOwner        sdk.AccAddress `json:"cdp_owner"`
	CollateralDenom string         `json:"collateral_denom"`
}
```
## nft

#### type MsgBurnNFT

```go
type MsgBurnNFT struct {
	Sender sdk.AccAddress `json:"sender" yaml:"sender"`
	ID     string         `json:"id" yaml:"id"`
	Denom  string         `json:"denom" yaml:"denom"`
}
```

MsgBurnNFT defines a BurnNFT message

#### type MsgEditNFTMetadata

```go
type MsgEditNFTMetadata struct {
	Sender   sdk.AccAddress `json:"sender" yaml:"sender"`
	ID       string         `json:"id" yaml:"id"`
	Denom    string         `json:"denom" yaml:"denom"`
	TokenURI string         `json:"token_uri" yaml:"token_uri"`
}
```

MsgEditNFTMetadata edits an NFT's metadata

#### type MsgMintNFT

```go
type MsgMintNFT struct {
	Sender    sdk.AccAddress `json:"sender" yaml:"sender"`
	Recipient sdk.AccAddress `json:"recipient" yaml:"recipient"`
	ID        string         `json:"id" yaml:"id"`
	Denom     string         `json:"denom" yaml:"denom"`
	TokenURI  string         `json:"token_uri" yaml:"token_uri"`
}
```

MsgMintNFT defines a MintNFT message

#### type MsgTransferNFT

```go
type MsgTransferNFT struct {
	Sender    sdk.AccAddress `json:"sender" yaml:"sender"`
	Recipient sdk.AccAddress `json:"recipient" yaml:"recipient"`
	Denom     string         `json:"denom" yaml:"denom"`
	ID        string         `json:"id" yaml:"id"`
}
```

MsgTransferNFT defines a TransferNFT message

## oracle

#### type MsgPostPrice

```go
type MsgPostPrice struct {
	From      sdk.AccAddress `json:"from" yaml:"from"`
	AssetCode string         `json:"asset_code" yaml:"asset_code"`
	Price     sdk.Dec        `json:"price" yaml:"price"`
	Expiry    time.Time      `json:"expiry" yaml:"expiry"`
}
```

MsgPostPrice struct representing a posted price message. Used by oracles to
input prices to the oracle

## order

#### type MsgPost

```go
type MsgPost struct {
	Owner       sdk.AccAddress     `json:"owner" yaml:"owner"`
	MarketID    store.EntityID     `json:"market_id" yaml:"market_id"`
	Direction   matcheng.Direction `json:"direction" yaml:"direction"`
	Price       sdk.Uint           `json:"price" yaml:"price"`
	Quantity    sdk.Uint           `json:"quantity" yaml:"quantity"`
	TimeInForce uint16             `json:"time_in_force" yaml:"time_in_force"`
}
```

## record

#### type MsgRecord

```go
type MsgRecord struct {
	Sender        sdk.AccAddress `json:"sender" yaml:"sender"`
	*RecordParams `json:"params" yaml:"params"`
}
```

MsgRecord to allow a registered recordr to record new coins.

## synthetic

#### type MsgBuySynthetic

```go
type MsgBuySynthetic struct {
	Sender sdk.AccAddress `json:"sender" yaml:"sender"`
	Coin   sdk.Coin       `json:"coin" yaml:"coin"`
}
```

MsgBuySynthetic purchases a synthetic position

#### type MsgSellSynthetic

```go
type MsgSellSynthetic struct {
	Sender sdk.AccAddress `json:"sender" yaml:"sender"`
	Coin   sdk.Coin       `json:"coin" yaml:"coin"`
}
```

MsgSellSynthetic purchases a synthetic position
