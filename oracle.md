# types
--
    import "github.com/xar-network/xar-network/x/oracle/internal/types"


## Usage

```go
const (
	// DefaultCodespace codespace for the module
	DefaultCodespace sdk.CodespaceType = ModuleName

	// CodeEmptyInput error code for empty input errors
	CodeEmptyInput sdk.CodeType = 1
	// CodeExpired error code for expired prices
	CodeExpired sdk.CodeType = 2
	// CodeInvalidPrice error code for all input prices expired
	CodeInvalidPrice sdk.CodeType = 3
	// CodeInvalidAsset error code for invalid asset
	CodeInvalidAsset sdk.CodeType = 4
	// CodeInvalidOracle error code for invalid oracle
	CodeInvalidOracle sdk.CodeType = 5
)
```

```go
const (
	// ModuleKey is the name of the module
	ModuleName = "oracle"

	// StoreKey is the store key string for gov
	StoreKey = ModuleName

	// RouterKey is the message route for gov
	RouterKey = ModuleName

	// QuerierRoute is the querier route for gov
	QuerierRoute = ModuleName

	// Parameter store default namestore
	DefaultParamspace = ModuleName

	// Store prefix for the raw oracle of an asset
	RawPriceFeedPrefix = StoreKey + ":raw:"

	// Store prefix for the current price of an asset
	CurrentPricePrefix = StoreKey + ":currentprice:"

	// Store Prefix for the assets in the oracle system
	AssetPrefix = StoreKey + ":assets"

	// OraclePrefix store prefix for the oracle accounts
	OraclePrefix = StoreKey + ":oracles"
)
```

```go
const (
	// QueryCurrentPrice command for current price queries
	QueryCurrentPrice = "price"
	// QueryRawPrices command for raw price queries
	QueryRawPrices = "rawprices"
	// QueryAssets command for assets query
	QueryAssets = "assets"
)
```

```go
const (
	// TypeMsgPostPrice type of PostPrice msg
	TypeMsgPostPrice = "post_price"
)
```

```go
var (
	// KeyAssets store key for assets
	KeyAssets   = []byte("oracleassets")
	KeyNominees = []byte("oraclenominees")
)
```

```go
var ModuleCdc *codec.Codec
```
generic sealed codec to be used throughout module

#### func  ErrEmptyInput

```go
func ErrEmptyInput(codespace sdk.CodespaceType) sdk.Error
```
ErrEmptyInput Error constructor

#### func  ErrExistingAsset

```go
func ErrExistingAsset(codespace sdk.CodespaceType) sdk.Error
```
ErrExistingAsset Error constructor for posted price messages for invalid assets

#### func  ErrExpired

```go
func ErrExpired(codespace sdk.CodespaceType) sdk.Error
```
ErrExpired Error constructor for posted price messages with expired price

#### func  ErrInvalidAsset

```go
func ErrInvalidAsset(codespace sdk.CodespaceType) sdk.Error
```
ErrInvalidAsset Error constructor for posted price messages for invalid assets

#### func  ErrInvalidOracle

```go
func ErrInvalidOracle(codespace sdk.CodespaceType) sdk.Error
```
ErrInvalidOracle Error constructor for posted price messages for invalid oracles

#### func  ErrNoValidPrice

```go
func ErrNoValidPrice(codespace sdk.CodespaceType) sdk.Error
```
ErrNoValidPrice Error constructor for posted price messages with expired price

#### func  ParamKeyTable

```go
func ParamKeyTable() params.KeyTable
```
ParamKeyTable Key declaration for parameters

#### func  RegisterCodec

```go
func RegisterCodec(cdc *codec.Codec)
```
RegisterCodec registers concrete types on the Amino codec

#### func  ValidateAddress

```go
func ValidateAddress(address string) (sdk.AccAddress, error)
```

#### func  ValidateGenesis

```go
func ValidateGenesis(data GenesisState) error
```
ValidateGenesis performs basic validation of genesis data returning an error for
any failed validation criteria.

#### type Asset

```go
type Asset struct {
	AssetCode  string  `json:"asset_code" yaml:"asset_code"`
	BaseAsset  string  `json:"base_asset" yaml:"base_asset"`
	QuoteAsset string  `json:"quote_asset" yaml:"quote_asset"`
	Oracles    Oracles `json:"oracles" yaml:"oracles"`
	Active     bool    `json:"active" yaml:"active"`
}
```

Asset struct that represents an asset in the oracle

#### func  NewAsset

```go
func NewAsset(
	assetCode, baseAsset, quoteAsset string,
	oracles Oracles,
	active bool,
) Asset
```
NewAsset creates a new asset

#### func (Asset) String

```go
func (a Asset) String() string
```
implement fmt.Stringer

#### func (Asset) ValidateBasic

```go
func (a Asset) ValidateBasic() sdk.Error
```
ValidateBasic does a simple validation check that doesn't require access to any
other information.

#### type Assets

```go
type Assets []Asset
```

Assets array type for oracle

#### func (Assets) String

```go
func (as Assets) String() string
```
String implements fmt.Stringer

#### type CurrentPrice

```go
type CurrentPrice struct {
	AssetCode string  `json:"asset_code" yaml:"asset_code"`
	Price     sdk.Dec `json:"price" yaml:"price"`
}
```

CurrentPrice struct that contains the metadata of a current price for a
particular asset in the oracle module.

#### func (CurrentPrice) String

```go
func (cp CurrentPrice) String() string
```
implement fmt.Stringer

#### type GenesisState

```go
type GenesisState struct {
	Params       Params        `json:"asset_params" yaml:"asset_params"`
	PostedPrices []PostedPrice `json:"posted_prices" yaml:"posted_prices"`
}
```

GenesisState - oracle state that must be provided at genesis

#### func  DefaultGenesisState

```go
func DefaultGenesisState() GenesisState
```
DefaultGenesisState defines default GenesisState for oracle

#### func  NewGenesisState

```go
func NewGenesisState(p Params, pp []PostedPrice) GenesisState
```
NewGenesisState creates a new genesis state for the oracle module

#### func (GenesisState) Equal

```go
func (data GenesisState) Equal(data2 GenesisState) bool
```
Equal checks whether two gov GenesisState structs are equivalent

#### func (GenesisState) IsEmpty

```go
func (data GenesisState) IsEmpty() bool
```
IsEmpty returns true if a GenesisState is empty

#### type MsgAddAsset

```go
type MsgAddAsset struct {
	Nominee sdk.AccAddress `json:"nominee" yaml:"nominee"`
	Denom   string         `json:"denom" yaml:"denom"`
	Asset   Asset          `json:"asset" yaml:"asset"`
}
```

MsgAddAsset struct representing a new nominee based oracle

#### func  NewMsgAddAsset

```go
func NewMsgAddAsset(
	nominee sdk.AccAddress,
	denom string,
	asset Asset,
) MsgAddAsset
```
NewMsgAddAsset creates a new add oracle message

#### func (MsgAddAsset) GetSignBytes

```go
func (msg MsgAddAsset) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgAddAsset) GetSigners

```go
func (msg MsgAddAsset) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgAddAsset) Route

```go
func (msg MsgAddAsset) Route() string
```
Route Implements Msg.

#### func (MsgAddAsset) Type

```go
func (msg MsgAddAsset) Type() string
```
Type Implements Msg

#### func (MsgAddAsset) ValidateBasic

```go
func (msg MsgAddAsset) ValidateBasic() sdk.Error
```
ValidateBasic does a simple validation check that doesn't require access to any
other information.

#### type MsgAddOracle

```go
type MsgAddOracle struct {
	Oracle  sdk.AccAddress `json:"oracle" yaml:"oracle"`
	Nominee sdk.AccAddress `json:"nominee" yaml:"nominee"`
	Denom   string         `json:"denom" yaml:"denom"`
}
```

MsgAddOracle struct representing a new nominee based oracle

#### func  NewMsgAddOracle

```go
func NewMsgAddOracle(
	nominee sdk.AccAddress,
	denom string,
	oracle sdk.AccAddress,
) MsgAddOracle
```
MsgAddOracle creates a new add oracle message

#### func (MsgAddOracle) GetSignBytes

```go
func (msg MsgAddOracle) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgAddOracle) GetSigners

```go
func (msg MsgAddOracle) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgAddOracle) Route

```go
func (msg MsgAddOracle) Route() string
```
Route Implements Msg.

#### func (MsgAddOracle) Type

```go
func (msg MsgAddOracle) Type() string
```
Type Implements Msg

#### func (MsgAddOracle) ValidateBasic

```go
func (msg MsgAddOracle) ValidateBasic() sdk.Error
```
ValidateBasic does a simple validation check that doesn't require access to any
other information.

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

#### func  NewMsgPostPrice

```go
func NewMsgPostPrice(
	from sdk.AccAddress,
	assetCode string,
	price sdk.Dec,
	expiry time.Time) MsgPostPrice
```
NewMsgPostPrice creates a new post price msg

#### func (MsgPostPrice) GetSignBytes

```go
func (msg MsgPostPrice) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgPostPrice) GetSigners

```go
func (msg MsgPostPrice) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgPostPrice) Route

```go
func (msg MsgPostPrice) Route() string
```
Route Implements Msg.

#### func (MsgPostPrice) Type

```go
func (msg MsgPostPrice) Type() string
```
Type Implements Msg

#### func (MsgPostPrice) ValidateBasic

```go
func (msg MsgPostPrice) ValidateBasic() sdk.Error
```
ValidateBasic does a simple validation check that doesn't require access to any
other information.

#### type MsgSetAsset

```go
type MsgSetAsset struct {
	Nominee sdk.AccAddress `json:"nominee" yaml:"nominee"`
	Denom   string         `json:"denom" yaml:"denom"`
	Asset   Asset          `json:"asset" yaml:"asset"`
}
```

MsgSetAsset struct representing a new nominee based oracle

#### func  NewMsgSetAsset

```go
func NewMsgSetAsset(
	nominee sdk.AccAddress,
	denom string,
	asset Asset,
) MsgSetAsset
```
NewMsgSetAsset creates a new add oracle message

#### func (MsgSetAsset) GetSignBytes

```go
func (msg MsgSetAsset) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgSetAsset) GetSigners

```go
func (msg MsgSetAsset) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgSetAsset) Route

```go
func (msg MsgSetAsset) Route() string
```
Route Implements Msg.

#### func (MsgSetAsset) Type

```go
func (msg MsgSetAsset) Type() string
```
Type Implements Msg

#### func (MsgSetAsset) ValidateBasic

```go
func (msg MsgSetAsset) ValidateBasic() sdk.Error
```
ValidateBasic does a simple validation check that doesn't require access to any
other information.

#### type MsgSetOracles

```go
type MsgSetOracles struct {
	Oracles Oracles        `json:"oracles" yaml:"oracles"`
	Nominee sdk.AccAddress `json:"nominee" yaml:"nominee"`
	Denom   string         `json:"denom" yaml:"denom"`
}
```

MsgSetOracle struct representing a new nominee based oracle

#### func  NewMsgSetOracles

```go
func NewMsgSetOracles(
	nominee sdk.AccAddress,
	denom string,
	oracles Oracles,
) MsgSetOracles
```
MsgAddOracle creates a new add oracle message

#### func (MsgSetOracles) GetSignBytes

```go
func (msg MsgSetOracles) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgSetOracles) GetSigners

```go
func (msg MsgSetOracles) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgSetOracles) Route

```go
func (msg MsgSetOracles) Route() string
```
Route Implements Msg.

#### func (MsgSetOracles) Type

```go
func (msg MsgSetOracles) Type() string
```
Type Implements Msg

#### func (MsgSetOracles) ValidateBasic

```go
func (msg MsgSetOracles) ValidateBasic() sdk.Error
```
ValidateBasic does a simple validation check that doesn't require access to any
other information.

#### type Oracle

```go
type Oracle struct {
	Address sdk.AccAddress `json:"address" yaml:"address"`
}
```

Oracle struct that documents which address an oracle is using

#### func  NewOracle

```go
func NewOracle(address sdk.AccAddress) Oracle
```

#### func (Oracle) String

```go
func (o Oracle) String() string
```
String implements fmt.Stringer

#### type Oracles

```go
type Oracles []Oracle
```

Oracles array type for oracle

#### func  ParseOracles

```go
func ParseOracles(addresses string) (Oracles, error)
```

#### func (Oracles) String

```go
func (os Oracles) String() string
```
String implements fmt.Stringer

#### type ParamSubspace

```go
type ParamSubspace interface {
	Get(ctx sdk.Context, key []byte, ptr interface{})
	Set(ctx sdk.Context, key []byte, param interface{})
}
```

ParamSubspace defines the expected Subspace interface for parameters

#### type Params

```go
type Params struct {
	Assets   []Asset  `json:"assets" yaml:"assets"` //  Array containing the assets supported by the oracle
	Nominees []string `json:"nominees" yaml:"nominees"`
}
```

Params params for oracle. Can be altered via governance

#### func  DefaultParams

```go
func DefaultParams() Params
```
DefaultParams default params for oracle

#### func  NewParams

```go
func NewParams(assets []Asset, nominees []string) Params
```
NewParams creates a new AssetParams object

#### func (Params) ParamSetPairs

```go
func (p Params) ParamSetPairs() params.ParamSetPairs
```
ParamSetPairs implements the ParamSet interface and returns all the key/value
pairs pairs of oracle module's parameters.

#### func (Params) String

```go
func (p Params) String() string
```
String implements fmt.stringer

#### func (Params) Validate

```go
func (p Params) Validate() error
```
Validate ensure that params have valid values

#### type PendingPriceAsset

```go
type PendingPriceAsset struct {
	AssetCode string `json:"asset_code"`
}
```

PendingPriceAsset struct that contains the info about the asset which price is
still to be determined

#### func (PendingPriceAsset) String

```go
func (a PendingPriceAsset) String() string
```
implement fmt.Stringer

#### type PostedPrice

```go
type PostedPrice struct {
	AssetCode     string         `json:"asset_code" yaml:"asset_code"`
	OracleAddress sdk.AccAddress `json:"oracle_address" yaml:"oracle_address"`
	Price         sdk.Dec        `json:"price" yaml:"price"`
	Expiry        time.Time      `json:"expiry" yaml:"expiry"`
}
```

PostedPrice struct represented a price for an asset posted by a specific oracle

#### func (PostedPrice) String

```go
func (pp PostedPrice) String() string
```
implement fmt.Stringer

#### type QueryAssetsResp

```go
type QueryAssetsResp []string
```

QueryAssetsResp response to a assets query

#### func (QueryAssetsResp) String

```go
func (n QueryAssetsResp) String() string
```
implement fmt.Stringer

#### type QueryRawPricesResp

```go
type QueryRawPricesResp []string
```

QueryRawPricesResp response to a rawprice query

#### func (QueryRawPricesResp) String

```go
func (n QueryRawPricesResp) String() string
```
implement fmt.Stringer

#### type SortDecs

```go
type SortDecs []sdk.Dec
```

SortDecs provides the interface needed to sort sdk.Dec slices

#### func (SortDecs) Len

```go
func (a SortDecs) Len() int
```

#### func (SortDecs) Less

```go
func (a SortDecs) Less(i, j int) bool
```

#### func (SortDecs) Swap

```go
func (a SortDecs) Swap(i, j int)
```
