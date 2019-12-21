# types
--
    import "github.com/xar-network/xar-network/x/synthetic/internal/types"


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
	ModuleName = "synthetic"
	// StoreKey is the store key string for issue
	StoreKey = ModuleName
	// RouterKey is the message route for issue
	RouterKey = ModuleName
	// QuerierRoute is the querier route for issue
	QuerierRoute = ModuleName
	// Parameter store default namestore
	DefaultParamspace = ModuleName

	DefaultCodespace sdk.CodespaceType = ModuleName

	// StableDenom asset code of the dollar-denominated debt coin
	StableDenom = "ucsdt" // TODO allow to be changed
	// GovDenom asset code of the governance coin
	GovDenom = "uftm"
)
```

```go
const (
	IncorrectBaseAmountForFeeCode = 101 + iota
)
```

```go
const (
	QueryGetParams = "params"
)
```

```go
var (
	KeySyntheticParams     = []byte("SyntheticParams")
	KeyNominees            = []byte("Nominees")
	DefaultSyntheticParams = SyntheticParams{SyntheticParam{
		Denom: "sbtc",
	}}
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


#### type GenesisState

```go
type GenesisState struct {
	Params Params `json:"params" yaml:"params"`
}
```


#### func  DefaultGenesisState

```go
func DefaultGenesisState() GenesisState
```
DefaultGenesisState returns a default genesis state

#### type MsgBuySynthetic

```go
type MsgBuySynthetic struct {
	Sender sdk.AccAddress `json:"sender" yaml:"sender"`
	Coin   sdk.Coin       `json:"coin" yaml:"coin"`
}
```

MsgBuySynthetic purchases a synthetic position

#### func  NewMsgBuySynthetic

```go
func NewMsgBuySynthetic(sender sdk.AccAddress, coin sdk.Coin) MsgBuySynthetic
```
NewMsgBuySynthetic returns a new MsgBuySynthetic.

#### func (MsgBuySynthetic) GetSignBytes

```go
func (msg MsgBuySynthetic) GetSignBytes() []byte
```
GetSignBytes gets the canonical byte representation of the Msg.

#### func (MsgBuySynthetic) GetSigners

```go
func (msg MsgBuySynthetic) GetSigners() []sdk.AccAddress
```
GetSigners returns the addresses of signers that must sign.

#### func (MsgBuySynthetic) Route

```go
func (msg MsgBuySynthetic) Route() string
```
Route return the message type used for routing the message.

#### func (MsgBuySynthetic) Type

```go
func (msg MsgBuySynthetic) Type() string
```
Type returns a human-readable string for the message, intended for utilization
within tags.

#### func (MsgBuySynthetic) ValidateBasic

```go
func (msg MsgBuySynthetic) ValidateBasic() sdk.Error
```
ValidateBasic does a simple validation check that doesn't require access to any
other information.

#### type MsgSellSynthetic

```go
type MsgSellSynthetic struct {
	Sender sdk.AccAddress `json:"sender" yaml:"sender"`
	Coin   sdk.Coin       `json:"coin" yaml:"coin"`
}
```

MsgSellSynthetic purchases a synthetic position

#### func  NewMsgSellSynthetic

```go
func NewMsgSellSynthetic(sender sdk.AccAddress, coin sdk.Coin) MsgSellSynthetic
```
NewMsgSellSynthetic returns a new MsgSellSynthetic.

#### func (MsgSellSynthetic) GetSignBytes

```go
func (msg MsgSellSynthetic) GetSignBytes() []byte
```
GetSignBytes gets the canonical byte representation of the Msg.

#### func (MsgSellSynthetic) GetSigners

```go
func (msg MsgSellSynthetic) GetSigners() []sdk.AccAddress
```
GetSigners returns the addresses of signers that must sign.

#### func (MsgSellSynthetic) Route

```go
func (msg MsgSellSynthetic) Route() string
```
Route return the message type used for routing the message.

#### func (MsgSellSynthetic) Type

```go
func (msg MsgSellSynthetic) Type() string
```
Type returns a human-readable string for the message, intended for utilization
within tags.

#### func (MsgSellSynthetic) ValidateBasic

```go
func (msg MsgSellSynthetic) ValidateBasic() sdk.Error
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
	SyntheticParams SyntheticParams `json:"synthetic_params" yaml:"synthetic_params"`
	Nominees        []string        `json:"nominees" yaml:"nominees"`
	Fee             fee.Fee         `json:"fee" yaml:"fee"`
}
```

Params governance parameters for synthetic module

#### func  DefaultParams

```go
func DefaultParams() Params
```
DefaultParams returns default params for synthetic module

#### func  NewParams

```go
func NewParams(
	syntheticParams SyntheticParams,
	nominees []string,
	fee fee.Fee,
) Params
```
NewParams returns a new params object

#### func (Params) GetSyntheticParam

```go
func (p Params) GetSyntheticParam(denom string) SyntheticParam
```

#### func (Params) IsSyntheticPresent

```go
func (p Params) IsSyntheticPresent(denom string) bool
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


#### type SyntheticParam

```go
type SyntheticParam struct {
	Denom string `json:"denom" yaml:"denom"`
}
```


#### func (SyntheticParam) String

```go
func (sp SyntheticParam) String() string
```
String implements fmt.Stringer

#### type SyntheticParams

```go
type SyntheticParams []SyntheticParam
```

SyntheticParams array of SyntheticParam

#### func (SyntheticParams) String

```go
func (sps SyntheticParams) String() string
```
String implements fmt.Stringer
