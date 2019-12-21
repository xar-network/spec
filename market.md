# types
--
    import "github.com/xar-network/xar-network/x/market/types"


## Usage

```go
const (
	// DefaultCodespace codespace for the module
	DefaultCodespace sdk.CodespaceType = ModuleName

	// CodeEmptyInput error code for empty input errors
	CodeNoPOA sdk.CodeType = 1
)
```

```go
const (
	// ModuleName The name that will be used throughout the module
	ModuleName = "market"

	// StoreKey Top level store key where all module items will be stored
	StoreKey = ModuleName

	// RouterKey Top level router key
	RouterKey = ModuleName

	// DefaultParamspace default name for parameter store
	DefaultParamspace = ModuleName

	ModuleNominees = "marketnominees"
)
```

```go
var (
	// ParamStoreKeyAuctionParams Param store key for auction params
	KeyMarkets  = []byte(ModuleName)
	KeyNominees = []byte(ModuleNominees)
)
```
Parameter keys

```go
var ModuleCdc *codec.Codec
```

#### func  ErrNoPOA

```go
func ErrNoPOA(codespace sdk.CodespaceType) sdk.Error
```
ErrEmptyInput Error constructor

#### func  ParamKeyTable

```go
func ParamKeyTable() subspace.KeyTable
```
ParamKeyTable Key declaration for parameters

#### func  RegisterCodec

```go
func RegisterCodec(cdc *codec.Codec)
```

#### type ListQueryResult

```go
type ListQueryResult struct {
	Markets []NamedMarket `json:"markets"`
}
```


#### func (ListQueryResult) String

```go
func (l ListQueryResult) String() string
```

#### type Market

```go
type Market struct {
	ID              store.EntityID `json:"id" yaml:"id"`
	BaseAssetDenom  string         `json:"base_asset_denom" yaml:"base_asset_denom"`
	QuoteAssetDenom string         `json:"quote_asset_denom" yaml:"quote_asset_denom"`
}
```


#### func  NewMarket

```go
func NewMarket(
	id store.EntityID,
	baseAsset string,
	quoteAsset string,
) Market
```

#### func (Market) String

```go
func (m Market) String() string
```
implement fmt.Stringer

#### type Markets

```go
type Markets []Market
```


#### type MsgCreateMarket

```go
type MsgCreateMarket struct {
	Nominee    sdk.AccAddress `json:"nominee" yaml:"nominee"`
	BaseAsset  string         `json:"base_asset" yaml:"base_asset"`
	QuoteAsset string         `json:"quote_asset" yaml:"quote_asset"`
}
```


#### func  NewMsgCreateMarket

```go
func NewMsgCreateMarket(
	nominee sdk.AccAddress,
	baseAsset string,
	quoteAsset string,
) MsgCreateMarket
```

#### func (MsgCreateMarket) GetSignBytes

```go
func (msg MsgCreateMarket) GetSignBytes() []byte
```

#### func (MsgCreateMarket) GetSigners

```go
func (msg MsgCreateMarket) GetSigners() []sdk.AccAddress
```

#### func (MsgCreateMarket) Route

```go
func (msg MsgCreateMarket) Route() string
```

#### func (MsgCreateMarket) Type

```go
func (msg MsgCreateMarket) Type() string
```

#### func (MsgCreateMarket) ValidateBasic

```go
func (msg MsgCreateMarket) ValidateBasic() sdk.Error
```

#### type NamedMarket

```go
type NamedMarket struct {
	ID              string
	BaseAssetDenom  string
	QuoteAssetDenom string
	Name            string
}
```


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
	Markets  []Market
	Nominees []string
}
```


#### func  DefaultParams

```go
func DefaultParams() Params
```
DefaultParams default params

#### func  NewParams

```go
func NewParams(markets []Market, nominees []string) Params
```
NewParams creates a new Params object

#### func (*Params) ParamSetPairs

```go
func (p *Params) ParamSetPairs() subspace.ParamSetPairs
```
ParamSetPairs implements the ParamSet interface and returns all the key/value
pairs pairs of auth module's parameters. nolint

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
