# csdt
--
    import "github.com/xar-network/xar-network/x/csdt/internal/types"

Package CSDT manages the storage of Collateralized Stable Debt Tokens. It
handles their creation, modification, and stores the global state of all CSDTs.

## Usage

```go
const (
	MsgIncorrectBaseAmountForFee = "base fee amount cannot be less or equal to zero"
	MsgIncorrectMinimumFee       = "minimum fee cannot be less than zero"
)
```

```go
const (
	// ModuleKey is the name of the module
	ModuleName = "csdt"
	// StoreKey is the store key string for issue
	StoreKey = ModuleName
	// RouterKey is the message route for issue
	RouterKey = ModuleName
	// QuerierRoute is the querier route for issue
	QuerierRoute = ModuleName
	// Parameter store default namestore
	DefaultParamspace = ModuleName

	// StableDenom asset code of the dollar-denominated debt coin
	StableDenom = "ucsdt" // TODO allow to be changed
	// GovDenom asset code of the governance coin
	GovDenom                           = "uftm"
	DefaultCodespace sdk.CodespaceType = ModuleName
)
```

```go
const (
	QueryGetCsdts             = "cdts"
	QueryGetParams            = "params"
	RestOwner                 = "owner"
	RestCollateralDenom       = "collateralDenom"
	RestUnderCollateralizedAt = "underCollateralizedAt"
)
```

```go
const (
	IncorrectBaseAmountForFeeCode = 101 + iota
)
```

```go
var (
	// ParamStoreKeyAuctionParams Param store key for auction params
	KeyGlobalDebtLimit      = []byte("GlobalDebtLimit")
	KeyCollateralParams     = []byte("CollateralParams")
	KeyDebtParams           = []byte("DebtParams")
	KeyCircuitBreaker       = []byte("CircuitBreaker")
	KeyNominees             = []byte("Nominees")
	DefaultGlobalDebt       = sdk.NewCoins(sdk.NewCoin(StableDenom, sdk.NewInt(500000000000)))
	DefaultCircuitBreaker   = false
	DefaultCollateralParams = CollateralParams{CollateralParam{
		Denom:            "uftm",
		LiquidationRatio: sdk.MustNewDecFromStr("1.5"),
		DebtLimit:        sdk.NewCoins(sdk.NewCoin(StableDenom, sdk.NewInt(500000000000))),
	}}
	DefaultDebtParams = DebtParams{}
)
```
Parameter keys

```go
var ErrIncorrectBaseAmountForFee = sdk.NewError(DefaultCodespace, IncorrectBaseAmountForFeeCode, MsgIncorrectBaseAmountForFee)
```

```go
var ModuleCdc *codec.Codec
```
generic sealed codec to be used throughout module

#### func  ParamKeyTable

```go
func ParamKeyTable() params.KeyTable
```
ParamKeyTable Key declaration for parameters

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

#### type BankKeeper

```go
type BankKeeper interface {
	GetCoins(sdk.Context, sdk.AccAddress) sdk.Coins
	HasCoins(sdk.Context, sdk.AccAddress, sdk.Coins) bool
	AddCoins(sdk.Context, sdk.AccAddress, sdk.Coins) (sdk.Coins, sdk.Error)
	SubtractCoins(sdk.Context, sdk.AccAddress, sdk.Coins) (sdk.Coins, sdk.Error)
}
```


#### type ByCollateralRatio

```go
type ByCollateralRatio CSDTs
```

byCollateralRatio is used to sort CSDTs

#### func (ByCollateralRatio) Len

```go
func (csdts ByCollateralRatio) Len() int
```

#### func (ByCollateralRatio) Less

```go
func (csdts ByCollateralRatio) Less(i, j int) bool
```

#### func (ByCollateralRatio) Swap

```go
func (csdts ByCollateralRatio) Swap(i, j int)
```

#### type CSDT

```go
type CSDT struct {
	//ID             []byte                                    // removing IDs for now to make things simpler
	Owner            sdk.AccAddress `json:"owner" yaml:"owner"`                         // Account that authorizes changes to the CSDT
	CollateralDenom  string         `json:"collateral_denom" yaml:"collateral_denom"`   // Type of collateral stored in this CSDT
	CollateralAmount sdk.Coins      `json:"collateral_amount" yaml:"collateral_amount"` // Amount of collateral stored in this CSDT
	Debt             sdk.Coins      `json:"debt" yaml:"debt"`
	AccumulatedFees  sdk.Coins      `json:"accumulated_fees" yaml:"accumulated_fees"`
	FeesUpdated      time.Time      `json:"fees_updated" yaml:"fees_updated"` // Amount of stable coin drawn from this CSDT
}
```

CSDT is the state of a single account.

#### func (CSDT) IsUnderCollateralized

```go
func (csdt CSDT) IsUnderCollateralized(price sdk.Dec, liquidationRatio sdk.Dec) bool
```

#### func (CSDT) String

```go
func (csdt CSDT) String() string
```

#### type CSDTs

```go
type CSDTs []CSDT
```


#### func (CSDTs) String

```go
func (csdts CSDTs) String() string
```

#### type CollateralParam

```go
type CollateralParam struct {
	Denom            string    `json:"denom" yaml:"denom"`                         // Coin name of collateral type
	LiquidationRatio sdk.Dec   `json:"liquidation_ratio" yaml:"liquidation_ratio"` // The ratio (Collateral (priced in stable coin) / Debt) under which a CSDT will be liquidated
	DebtLimit        sdk.Coins `json:"debt_limit" yaml:"debt_limit"`               // Maximum amount of debt allowed to be drawn from this collateral type

}
```


#### func (CollateralParam) String

```go
func (cp CollateralParam) String() string
```
String implements fmt.Stringer

#### type CollateralParams

```go
type CollateralParams []CollateralParam
```

CollateralParams array of CollateralParam

#### func (CollateralParams) String

```go
func (cps CollateralParams) String() string
```
String implements fmt.Stringer

#### type CollateralState

```go
type CollateralState struct {
	Denom     string  // Type of collateral
	TotalDebt sdk.Int // total debt collateralized by a this coin type

}
```

CollateralState stores global information tied to a particular collateral type.

#### type DebtParam

```go
type DebtParam struct {
	Denom          string    `json:"denom" yaml:"denom"`
	ReferenceAsset string    `json:"reference_asset" yaml:"reference_asset"`
	DebtLimit      sdk.Coins `json:"debt_limit" yaml:"debt_limit"`
}
```

DebtParam governance params for debt assets

#### func (DebtParam) String

```go
func (dp DebtParam) String() string
```

#### type DebtParams

```go
type DebtParams []DebtParam
```

DebtParams array of DebtParam

#### func (DebtParams) String

```go
func (dps DebtParams) String() string
```
String implements fmt.Stringer

#### type GenesisState

```go
type GenesisState struct {
	Params Params `json:"params" yaml:"params"`
	CSDTs  CSDTs  `json:"csdts" yaml:"csdts"`
}
```


#### func  DefaultGenesisState

```go
func DefaultGenesisState() GenesisState
```
DefaultGenesisState returns a default genesis state TODO make this empty, load
test values independent

#### type ModifyCsdtRequestBody

```go
type ModifyCsdtRequestBody struct {
	BaseReq rest.BaseReq `json:"base_req"`
	Csdt    CSDT         `json:"csdt"`
}
```


#### type MsgAddCollateralParam

```go
type MsgAddCollateralParam struct {
	Nominee          sdk.AccAddress `json:"nominee" yaml:"nominee"`
	CollateralDenom  string         `json:"collateral_denom" yaml:"collateral_denom"`
	LiquidationRatio sdk.Dec        `json:"liquidation_ratio" yaml:"liquidation_ratio"`
	DebtLimit        sdk.Coins      `json:"debt_limit" yaml:"debt_limit"`
}
```

MsgAddCollateralParam adds collateral to CSDT management

#### func  NewMsgAddCollateralParam

```go
func NewMsgAddCollateralParam(
	nominee sdk.AccAddress,
	collateralDenom string,
	liquidationRatio sdk.Dec,
	debtLimit sdk.Coins,
) MsgAddCollateralParam
```
NewMsgAddCollateralParam returns a new MsgAddCollateralParam.

#### func (MsgAddCollateralParam) GetSignBytes

```go
func (msg MsgAddCollateralParam) GetSignBytes() []byte
```
GetSignBytes gets the canonical byte representation of the Msg.

#### func (MsgAddCollateralParam) GetSigners

```go
func (msg MsgAddCollateralParam) GetSigners() []sdk.AccAddress
```
GetSigners returns the addresses of signers that must sign.

#### func (MsgAddCollateralParam) Route

```go
func (msg MsgAddCollateralParam) Route() string
```
Route return the message type used for routing the message.

#### func (MsgAddCollateralParam) Type

```go
func (msg MsgAddCollateralParam) Type() string
```
Type returns a human-readable string for the message, intended for utilization
within tags.

#### func (MsgAddCollateralParam) ValidateBasic

```go
func (msg MsgAddCollateralParam) ValidateBasic() sdk.Error
```
ValidateBasic does a simple validation check that doesn't require access to any
other information.

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

#### func  NewMsgCreateOrModifyCSDT

```go
func NewMsgCreateOrModifyCSDT(sender sdk.AccAddress, collateralDenom string, collateralChange sdk.Int, debtChange sdk.Int) MsgCreateOrModifyCSDT
```
NewMsgCreateOrModifyCSDT returns a new MsgCreateOrModifyCSDT.

#### func (MsgCreateOrModifyCSDT) GetSignBytes

```go
func (msg MsgCreateOrModifyCSDT) GetSignBytes() []byte
```
GetSignBytes gets the canonical byte representation of the Msg.

#### func (MsgCreateOrModifyCSDT) GetSigners

```go
func (msg MsgCreateOrModifyCSDT) GetSigners() []sdk.AccAddress
```
GetSigners returns the addresses of signers that must sign.

#### func (MsgCreateOrModifyCSDT) Route

```go
func (msg MsgCreateOrModifyCSDT) Route() string
```
Route return the message type used for routing the message.

#### func (MsgCreateOrModifyCSDT) Type

```go
func (msg MsgCreateOrModifyCSDT) Type() string
```
Type returns a human-readable string for the message, intended for utilization
within tags.

#### func (MsgCreateOrModifyCSDT) ValidateBasic

```go
func (msg MsgCreateOrModifyCSDT) ValidateBasic() sdk.Error
```
ValidateBasic does a simple validation check that doesn't require access to any
other information.

#### type MsgDepositCollateral

```go
type MsgDepositCollateral struct {
	Sender           sdk.AccAddress `json:"sender" yaml:"sender"`
	CollateralDenom  string         `json:"collateral_denom" yaml:"collateral_denom"`
	CollateralChange sdk.Int        `json:"collateral_change" yaml:"collateral_change"`
}
```

MsgDepositCollateral adds collateral to CSDT.

#### func  NewMsgDepositCollateral

```go
func NewMsgDepositCollateral(sender sdk.AccAddress, collateralDenom string, collateralChange sdk.Int) MsgDepositCollateral
```
NewMsgDepositCollateral returns a new MsgDepositCollateral.

#### func (MsgDepositCollateral) GetSignBytes

```go
func (msg MsgDepositCollateral) GetSignBytes() []byte
```
GetSignBytes gets the canonical byte representation of the Msg.

#### func (MsgDepositCollateral) GetSigners

```go
func (msg MsgDepositCollateral) GetSigners() []sdk.AccAddress
```
GetSigners returns the addresses of signers that must sign.

#### func (MsgDepositCollateral) Route

```go
func (msg MsgDepositCollateral) Route() string
```
Route return the message type used for routing the message.

#### func (MsgDepositCollateral) Type

```go
func (msg MsgDepositCollateral) Type() string
```
Type returns a human-readable string for the message, intended for utilization
within tags.

#### func (MsgDepositCollateral) ValidateBasic

```go
func (msg MsgDepositCollateral) ValidateBasic() sdk.Error
```
ValidateBasic does a simple validation check that doesn't require access to any
other information.

#### type MsgSetCollateralParam

```go
type MsgSetCollateralParam struct {
	Nominee          sdk.AccAddress `json:"nominee" yaml:"nominee"`
	CollateralDenom  string         `json:"collateral_denom" yaml:"collateral_denom"`
	LiquidationRatio sdk.Dec        `json:"liquidation_ratio" yaml:"liquidation_ratio"`
	DebtLimit        sdk.Coins      `json:"debt_limit" yaml:"debt_limit"`
}
```

MsgSetCollateralParam sets collateral in CSDT management

#### func  NewMsgSetCollateralParam

```go
func NewMsgSetCollateralParam(
	nominee sdk.AccAddress,
	collateralDenom string,
	liquidationRatio sdk.Dec,
	debtLimit sdk.Coins,
) MsgSetCollateralParam
```
NewMsgSetCollateralParam returns a new MsgSetCollateralParam.

#### func (MsgSetCollateralParam) GetSignBytes

```go
func (msg MsgSetCollateralParam) GetSignBytes() []byte
```
GetSignBytes gets the canonical byte representation of the Msg.

#### func (MsgSetCollateralParam) GetSigners

```go
func (msg MsgSetCollateralParam) GetSigners() []sdk.AccAddress
```
GetSigners returns the addresses of signers that must sign.

#### func (MsgSetCollateralParam) Route

```go
func (msg MsgSetCollateralParam) Route() string
```
Route return the message type used for routing the message.

#### func (MsgSetCollateralParam) Type

```go
func (msg MsgSetCollateralParam) Type() string
```
Type returns a human-readable string for the message, intended for utilization
within tags.

#### func (MsgSetCollateralParam) ValidateBasic

```go
func (msg MsgSetCollateralParam) ValidateBasic() sdk.Error
```
ValidateBasic does a simple validation check that doesn't require access to any
other information.

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

#### func  NewMsgSettleDebt

```go
func NewMsgSettleDebt(sender sdk.AccAddress, collateralDenom, debtDenom string, debtChange sdk.Int) MsgSettleDebt
```
NewMsgSettleDebt returns a new MsgSettleDebt.

#### func (MsgSettleDebt) GetSignBytes

```go
func (msg MsgSettleDebt) GetSignBytes() []byte
```
GetSignBytes gets the canonical byte representation of the Msg.

#### func (MsgSettleDebt) GetSigners

```go
func (msg MsgSettleDebt) GetSigners() []sdk.AccAddress
```
GetSigners returns the addresses of signers that must sign.

#### func (MsgSettleDebt) Route

```go
func (msg MsgSettleDebt) Route() string
```
Route return the message type used for routing the message.

#### func (MsgSettleDebt) Type

```go
func (msg MsgSettleDebt) Type() string
```
Type returns a human-readable string for the message, intended for utilization
within tags.

#### func (MsgSettleDebt) ValidateBasic

```go
func (msg MsgSettleDebt) ValidateBasic() sdk.Error
```
ValidateBasic does a simple validation check that doesn't require access to any
other information.

#### type MsgTransferCSDT

```go
type MsgTransferCSDT struct {
}
```

MsgTransferCSDT changes the ownership of a csdt

#### type MsgWithdrawCollateral

```go
type MsgWithdrawCollateral struct {
	Sender           sdk.AccAddress `json:"sender" yaml:"sender"`
	CollateralDenom  string         `json:"collateral_denom" yaml:"collateral_denom"`
	CollateralChange sdk.Int        `json:"collateral_change" yaml:"collateral_change"`
}
```

MsgWithdrawCollateral removes collateral to CSDT.

#### func  NewMsgWithdrawCollateral

```go
func NewMsgWithdrawCollateral(sender sdk.AccAddress, collateralDenom string, collateralChange sdk.Int) MsgWithdrawCollateral
```
NewMsgWithdrawCollateral returns a new MsgWithdrawCollateral.

#### func (MsgWithdrawCollateral) GetSignBytes

```go
func (msg MsgWithdrawCollateral) GetSignBytes() []byte
```
GetSignBytes gets the canonical byte representation of the Msg.

#### func (MsgWithdrawCollateral) GetSigners

```go
func (msg MsgWithdrawCollateral) GetSigners() []sdk.AccAddress
```
GetSigners returns the addresses of signers that must sign.

#### func (MsgWithdrawCollateral) Route

```go
func (msg MsgWithdrawCollateral) Route() string
```
Route return the message type used for routing the message.

#### func (MsgWithdrawCollateral) Type

```go
func (msg MsgWithdrawCollateral) Type() string
```
Type returns a human-readable string for the message, intended for utilization
within tags.

#### func (MsgWithdrawCollateral) ValidateBasic

```go
func (msg MsgWithdrawCollateral) ValidateBasic() sdk.Error
```
ValidateBasic does a simple validation check that doesn't require access to any
other information.

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

#### func  NewMsgWithdrawDebt

```go
func NewMsgWithdrawDebt(sender sdk.AccAddress, collateralDenom, debtDenom string, debtChange sdk.Int) MsgWithdrawDebt
```
NewMsgWithdrawDebt returns a new MsgWithdrawDebt.

#### func (MsgWithdrawDebt) GetSignBytes

```go
func (msg MsgWithdrawDebt) GetSignBytes() []byte
```
GetSignBytes gets the canonical byte representation of the Msg.

#### func (MsgWithdrawDebt) GetSigners

```go
func (msg MsgWithdrawDebt) GetSigners() []sdk.AccAddress
```
GetSigners returns the addresses of signers that must sign.

#### func (MsgWithdrawDebt) Route

```go
func (msg MsgWithdrawDebt) Route() string
```
Route return the message type used for routing the message.

#### func (MsgWithdrawDebt) Type

```go
func (msg MsgWithdrawDebt) Type() string
```
Type returns a human-readable string for the message, intended for utilization
within tags.

#### func (MsgWithdrawDebt) ValidateBasic

```go
func (msg MsgWithdrawDebt) ValidateBasic() sdk.Error
```
ValidateBasic does a simple validation check that doesn't require access to any
other information.

#### type OracleKeeper

```go
type OracleKeeper interface {
	GetCurrentPrice(sdk.Context, string) oracle.CurrentPrice
	// These are used for testing TODO replace mockApp with keeper in tests to remove these
	AddAsset(sdk.Context, string, string, oracle.Asset) error
	SetPrice(sdk.Context, sdk.AccAddress, string, sdk.Dec, time.Time) (oracle.PostedPrice, sdk.Error)
	SetCurrentPrices(sdk.Context) sdk.Error
	SetParams(ctx sdk.Context, params oracle.Params)
}
```


#### type Params

```go
type Params struct {
	CollateralParams CollateralParams `json:"collateral_params" yaml:"collateral_params"`
	DebtParams       DebtParams       `json:"debt_params" yaml:"debt_params"`
	GlobalDebtLimit  sdk.Coins        `json:"global_debt_limit" yaml:"global_debt_limit"`
	CircuitBreaker   bool             `json:"circuit_breaker" yaml:"circuit_breaker"`
	Fee              fee.Fee          `json:"fee" yaml:"fee"`
	Nominees         []string         `json:"nominees" yaml:"nominees"`
}
```

Params governance parameters for cdp module

#### func  DefaultParams

```go
func DefaultParams() Params
```
DefaultParams returns default params for cdp module

#### func  NewParams

```go
func NewParams(
	debtLimit sdk.Coins,
	collateralParams CollateralParams,
	debtParams DebtParams,
	breaker bool,
	nominees []string,
	fee fee.Fee,
) Params
```
NewParams returns a new params object

#### func (Params) GetCollateralParam

```go
func (cps Params) GetCollateralParam(collateralDenom string) CollateralParam
```

#### func (Params) IsCollateralPresent

```go
func (cps Params) IsCollateralPresent(collateralDenom string) bool
```

#### func (*Params) ParamSetPairs

```go
func (p *Params) ParamSetPairs() params.ParamSetPairs
```
ParamSetPairs implements the ParamSet interface and returns all the key/value
pairs pairs of auth module's parameters. nolint

#### func (Params) String

```go
func (p Params) String() string
```
String implements fmt.Stringer

#### func (Params) Validate

```go
func (p Params) Validate() error
```
Validate checks that the parameters have valid values.

#### type QueryCsdtsParams

```go
type QueryCsdtsParams struct {
	CollateralDenom       string         // get CSDTs with this collateral denom
	Owner                 sdk.AccAddress // get CSDTs belonging to this owner
	UnderCollateralizedAt sdk.Dec        // get CSDTs that will be below the liquidation ratio when the collateral is at this price.
}
```


#### type SupplyKeeper

```go
type SupplyKeeper interface {
	GetSupply(ctx sdk.Context) (supply exported.SupplyI)
	SetSupply(ctx sdk.Context, supply exported.SupplyI)
	SendCoinsFromAccountToModule(ctx sdk.Context, senderAddr sdk.AccAddress, recipientModule string, amt sdk.Coins) sdk.Error
	SendCoinsFromModuleToAccount(ctx sdk.Context, senderModule string, recipientAddr sdk.AccAddress, amt sdk.Coins) sdk.Error
	BurnCoins(ctx sdk.Context, moduleName string, amt sdk.Coins) sdk.Error
	MintCoins(ctx sdk.Context, moduleName string, amt sdk.Coins) sdk.Error
}
```
