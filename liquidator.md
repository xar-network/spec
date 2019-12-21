# types
--
    import "github.com/xar-network/xar-network/x/liquidator/internal/types"

Package Liquidator settles bad debt from undercollateralized CSDTs by seizing
them and raising funds through auctions.

### Notes

     - Missing the debt queue thing from Vow
     - seized collateral and csdt are stored in the module account, but debt (aka Sin) is stored in keeper
     - The boundary between the liquidator and the csdt modules is messy.
    	- The CSDT type is used in liquidator
    	- csdt knows about seizing
    	- seizing of a CSDT is split across each module
    	- recording of debt is split across modules
    	- liquidator needs get access to stable and gov denoms from the csdt module

### TODO

    - Is returning unsold collateral to the CSDT owner rather than the CSDT a problem? It could prevent the CSDT from becoming safe again.
    - Add some kind of more complete test
    - Add constants for the module and route names
    - tags
    - custom error types, codespace

## Usage

```go
const (
	// ModuleKey is the name of the module
	ModuleName = "liquidator"
	// StoreKey is the store key string for issue
	StoreKey = ModuleName
	// RouterKey is the message route for issue
	RouterKey = ModuleName
	// QuerierRoute is the querier route for issue
	QuerierRoute = ModuleName
	// Parameter store default namestore
	DefaultParamspace = ModuleName

	QueryGetOutstandingDebt = "outstanding_debt" // Get the outstanding seized debt
)
```

```go
var (
	KeyDebtAuctionSize  = []byte("DebtAuctionSize")
	KeyCollateralParams = []byte("CollateralParams")
)
```
Parameter keys

```go
var ModuleCdc = codec.New()
```

```go
var ModuleParamsKey = []byte("LiquidatorModuleParams")
```

#### func  ParamKeyTable

```go
func ParamKeyTable() subspace.KeyTable
```
ParamKeyTable for the liquidator module

#### func  RegisterCodec

```go
func RegisterCodec(cdc *codec.Codec)
```
RegisterCodec registers concrete types on the codec.

#### func  ValidateGenesis

```go
func ValidateGenesis(data GenesisState) error
```
ValidateGenesis performs basic validation of genesis data returning an error for
any failed validation criteria.

#### type AuctionKeeper

```go
type AuctionKeeper interface {
	StartForwardAuction(sdk.Context, sdk.AccAddress, sdk.Coin, sdk.Coin) (auction.ID, sdk.Error)
	StartReverseAuction(sdk.Context, sdk.AccAddress, sdk.Coin, sdk.Coin) (auction.ID, sdk.Error)
	StartForwardReverseAuction(sdk.Context, sdk.AccAddress, sdk.Coin, sdk.Coin, sdk.AccAddress) (auction.ID, sdk.Error)
}
```


#### type BankKeeper

```go
type BankKeeper interface {
	GetCoins(sdk.Context, sdk.AccAddress) sdk.Coins
}
```


#### type CollateralParams

```go
type CollateralParams struct {
	Denom       string  `json:"denom" yaml:"denom"`
	AuctionSize sdk.Int `json:"auction_size" yaml:"auction_size"`
}
```

CollateralParams params storing information about each collateral for the
liquidator module

#### func (CollateralParams) String

```go
func (cp CollateralParams) String() string
```
String implements stringer interface

#### type CsdtKeeper

```go
type CsdtKeeper interface {
	GetCSDT(sdk.Context, sdk.AccAddress, string) (csdt.CSDT, bool)
	PartialSeizeCSDT(sdk.Context, sdk.AccAddress, string, sdk.Int, sdk.Int) sdk.Error
	ReduceGlobalDebt(sdk.Context, sdk.Int) sdk.Error
	GetStableDenom() string // TODO can this be removed somehow?
	GetGovDenom() string
}
```


#### type GenesisState

```go
type GenesisState struct {
	Params LiquidatorParams `json:"liquidator_params" yaml:"liquidator_params"`
}
```

GenesisState is the state that must be provided at genesis.

#### func  DefaultGenesisState

```go
func DefaultGenesisState() GenesisState
```
DefaultGenesisState returns a default genesis state TODO pick better values

#### type LiquidatorParams

```go
type LiquidatorParams struct {
	DebtAuctionSize sdk.Int `json:"debt_auction_size" yaml:"debt_auction_size"`
	//SurplusAuctionSize sdk.Int
	CollateralParams []CollateralParams `json:"collateral_params" yaml:"collateral_params"`
}
```

LiquidatorParams store params for the liquidator module

#### func  DefaultParams

```go
func DefaultParams() LiquidatorParams
```
DefaultParams for the liquidator module

#### func  NewLiquidatorParams

```go
func NewLiquidatorParams(debtAuctionSize sdk.Int, collateralParams []CollateralParams) LiquidatorParams
```
NewLiquidatorParams returns a new params object for the liquidator module

#### func (*LiquidatorParams) ParamSetPairs

```go
func (p *LiquidatorParams) ParamSetPairs() subspace.ParamSetPairs
```
ParamSetPairs implements the ParamSet interface and returns all the key/value
pairs pairs of liquidator module's parameters. nolint

#### func (LiquidatorParams) String

```go
func (p LiquidatorParams) String() string
```
String implements fmt.Stringer

#### func (LiquidatorParams) Validate

```go
func (p LiquidatorParams) Validate() error
```

#### type MsgSeizeAndStartCollateralAuction

```go
type MsgSeizeAndStartCollateralAuction struct {
	Sender          sdk.AccAddress `json:"sender" yaml:"sender"`
	CsdtOwner       sdk.AccAddress `json:"owner" yaml:"owner"`
	CollateralDenom string         `json:"collateral_denom" yaml:"collateral_denom"`
}
```


#### func (MsgSeizeAndStartCollateralAuction) GetSignBytes

```go
func (msg MsgSeizeAndStartCollateralAuction) GetSignBytes() []byte
```
GetSignBytes gets the canonical byte representation of the Msg.

#### func (MsgSeizeAndStartCollateralAuction) GetSigners

```go
func (msg MsgSeizeAndStartCollateralAuction) GetSigners() []sdk.AccAddress
```
GetSigners returns the addresses of signers that must sign.

#### func (MsgSeizeAndStartCollateralAuction) Route

```go
func (msg MsgSeizeAndStartCollateralAuction) Route() string
```
Route return the message type used for routing the message.

#### func (MsgSeizeAndStartCollateralAuction) Type

```go
func (msg MsgSeizeAndStartCollateralAuction) Type() string
```
Type returns a human-readable string for the message, intended for utilization
within tags.

#### func (MsgSeizeAndStartCollateralAuction) ValidateBasic

```go
func (msg MsgSeizeAndStartCollateralAuction) ValidateBasic() sdk.Error
```
ValidateBasic does a simple validation check that doesn't require access to any
other information.

#### type MsgStartDebtAuction

```go
type MsgStartDebtAuction struct {
	Sender sdk.AccAddress `json:"sender" yaml:"sender"`
}
```


#### func (MsgStartDebtAuction) GetSignBytes

```go
func (msg MsgStartDebtAuction) GetSignBytes() []byte
```

#### func (MsgStartDebtAuction) GetSigners

```go
func (msg MsgStartDebtAuction) GetSigners() []sdk.AccAddress
```

#### func (MsgStartDebtAuction) Route

```go
func (msg MsgStartDebtAuction) Route() string
```

#### func (MsgStartDebtAuction) Type

```go
func (msg MsgStartDebtAuction) Type() string
```

#### func (MsgStartDebtAuction) ValidateBasic

```go
func (msg MsgStartDebtAuction) ValidateBasic() sdk.Error
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


#### type SeizedDebt

```go
type SeizedDebt struct {
	Total         sdk.Int // Total debt seized from CSDTs. Known as Awe in maker.
	SentToAuction sdk.Int // Portion of seized debt that has had a (reverse) auction was started for it. Known as Ash in maker.

}
```


#### func (SeizedDebt) Available

```go
func (sd SeizedDebt) Available() sdk.Int
```
Available gets the seized debt that has not been sent for auction. Known as Woe
in maker.

#### func (SeizedDebt) Settle

```go
func (sd SeizedDebt) Settle(amount sdk.Int) (SeizedDebt, sdk.Error)
```

#### type StartDebtAuctionRequest

```go
type StartDebtAuctionRequest struct {
	BaseReq rest.BaseReq   `json:"base_req"`
	Sender  sdk.AccAddress `json:"sender"` // TODO use baseReq.From instead?
}
```


#### type SupplyKeeper

```go
type SupplyKeeper interface {
	GetSupply(ctx sdk.Context) (supply exported.SupplyI)
	SetSupply(ctx sdk.Context, supply exported.SupplyI)
	SendCoinsFromAccountToModule(ctx sdk.Context, senderAddr sdk.AccAddress, recipientModule string, amt sdk.Coins) sdk.Error
	SendCoinsFromModuleToAccount(ctx sdk.Context, senderModule string, recipientAddr sdk.AccAddress, amt sdk.Coins) sdk.Error
	SendCoinsFromModuleToModule(ctx sdk.Context, senderModule, recipientModule string, amt sdk.Coins) sdk.Error
	GetModuleAddress(moduleName string) sdk.AccAddress
	BurnCoins(ctx sdk.Context, moduleName string, amt sdk.Coins) sdk.Error
	MintCoins(ctx sdk.Context, moduleName string, amt sdk.Coins) sdk.Error

	//testing
	GetModuleAddressAndPermissions(moduleName string) (addr sdk.AccAddress, permissions []string)
}
```
