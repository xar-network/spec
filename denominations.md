# denominations
--
    import "github.com/xar-network/xar-network/x/denominations/internal/types"


## Usage

```go
const (
	// DefaultCodespace codespace for the module
	DefaultCodespace sdk.CodespaceType = ModuleName

	// CodeEmptyInput error code for empty input errors
	CodeNoPOA sdk.CodeType = 1

	CodeTokenSymbolDoesNotExist sdk.CodeType = 101
)
```

```go
const (
	ModuleName = "denominations"

	QuerierRoute = ModuleName

	ModuleNominees = "nominees"
	// StoreKey Top level store key where all module items will be stored
	StoreKey = ModuleName

	// RouterKey Top level router key
	RouterKey = ModuleName

	// DefaultParamspace default name for parameter store
	DefaultParamspace = ModuleName
)
```

```go
var (
	KeyNominees = []byte(ModuleNominees)
)
```
Parameter keys

```go
var ModuleCdc *codec.Codec
```
generic sealed codec to be used throughout this module

#### func  AreAnyCoinsZero

```go
func AreAnyCoinsZero(coins *sdk.Coins) bool
```

#### func  ErrNoPOA

```go
func ErrNoPOA(codespace sdk.CodespaceType) sdk.Error
```
ErrEmptyInput Error constructor

#### func  ErrTokenSymbolDoesNotExist

```go
func ErrTokenSymbolDoesNotExist(codespace sdk.CodespaceType) sdk.Error
```

#### func  ParamKeyTable

```go
func ParamKeyTable() subspace.KeyTable
```
ParamKeyTable Key declaration for parameters

#### func  RegisterCodec

```go
func RegisterCodec(cdc *codec.Codec)
```

#### type CustomCoinAccount

```go
type CustomCoinAccount interface {
	exported.Account
	Freezer
}
```

CustomCoinAccount extends the built in account interface with extra abilities
such as frozen coins

#### type FreezeAccount

```go
type FreezeAccount struct {
	*authtypes.BaseAccount
	FrozenCoins sdk.Coins `json:"frozen" yaml:"frozen"`
}
```

FreezeAccount is customised to allow temporary freezing of coins to exclude them
from transactions

#### func  NewFreezeAccount

```go
func NewFreezeAccount(ba *authtypes.BaseAccount, frozenCoins sdk.Coins) *FreezeAccount
```

#### func (*FreezeAccount) FreezeCoins

```go
func (acc *FreezeAccount) FreezeCoins(coinsToFreeze sdk.Coins) error
```
FreezeCoins freezes unfrozen coins for account according to input

#### func (FreezeAccount) GetFrozenCoins

```go
func (acc FreezeAccount) GetFrozenCoins() sdk.Coins
```
GetFrozenCoins retrieves frozen coins from account

#### func (FreezeAccount) MarshalJSON

```go
func (acc FreezeAccount) MarshalJSON() ([]byte, error)
```
MarshalJSON returns the JSON representation of a ModuleAccount.

#### func (FreezeAccount) MarshalYAML

```go
func (acc FreezeAccount) MarshalYAML() (interface{}, error)
```
MarshalYAML returns the YAML representation of a ModuleAccount.

#### func (*FreezeAccount) SetFrozenCoins

```go
func (acc *FreezeAccount) SetFrozenCoins(frozen sdk.Coins) error
```
SetFrozenCoins sets frozen coins for account

#### func (FreezeAccount) String

```go
func (acc FreezeAccount) String() string
```

#### func (*FreezeAccount) UnfreezeCoins

```go
func (acc *FreezeAccount) UnfreezeCoins(coinsToUnfreeze sdk.Coins) error
```
UnfreezeCoins unfreezes frozen coins for account according to input

#### func (*FreezeAccount) UnmarshalJSON

```go
func (acc *FreezeAccount) UnmarshalJSON(bz []byte) error
```
UnmarshalJSON unmarshals raw JSON bytes into a ModuleAccount.

#### func (FreezeAccount) Validate

```go
func (acc FreezeAccount) Validate() error
```
Validate checks for errors on the account fields

#### type Freezer

```go
type Freezer interface {
	// Get just the frozen coins
	GetFrozenCoins() sdk.Coins
	SetFrozenCoins(sdk.Coins) error

	// Freeze coins by a certain amount. It will reduce amount of coins available from GetCoins()
	FreezeCoins(sdk.Coins) error
	// Unfreeze coins by a certain amount. It will increase the amount of coins available from GetCoins()
	UnfreezeCoins(sdk.Coins) error
}
```

Freezer allows setting and getting frozen coins

#### type MsgBurnCoins

```go
type MsgBurnCoins struct {
	Amount sdk.Int        `json:"amount" yaml:"amount"`
	Symbol string         `json:"symbol" yaml:"symbol"`
	Owner  sdk.AccAddress `json:"owner" yaml:"owner"`
}
```

MsgBurnCoins defines the BurnCoins message

#### func  NewMsgBurnCoins

```go
func NewMsgBurnCoins(amount sdk.Int, symbol string, owner sdk.AccAddress) MsgBurnCoins
```
NewMsgBurnCoins is the constructor function for MsgBurnCoins

#### func (MsgBurnCoins) GetSignBytes

```go
func (msg MsgBurnCoins) GetSignBytes() []byte
```
GetSignBytes encodes the message for signing

#### func (MsgBurnCoins) GetSigners

```go
func (msg MsgBurnCoins) GetSigners() []sdk.AccAddress
```
GetSigners defines whose signature is required

#### func (MsgBurnCoins) Route

```go
func (msg MsgBurnCoins) Route() string
```
Route should return the name of the module

#### func (MsgBurnCoins) Type

```go
func (msg MsgBurnCoins) Type() string
```
Type should return the action

#### func (MsgBurnCoins) ValidateBasic

```go
func (msg MsgBurnCoins) ValidateBasic() sdk.Error
```
ValidateBasic runs stateless checks on the message

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

#### func  NewMsgFreezeCoins

```go
func NewMsgFreezeCoins(amount sdk.Int, symbol string, owner sdk.AccAddress, address sdk.AccAddress) MsgFreezeCoins
```
NewMsgFreezeCoins is the constructor function for MsgFreezeCoins

#### func (MsgFreezeCoins) GetSignBytes

```go
func (msg MsgFreezeCoins) GetSignBytes() []byte
```
GetSignBytes encodes the message for signing

#### func (MsgFreezeCoins) GetSigners

```go
func (msg MsgFreezeCoins) GetSigners() []sdk.AccAddress
```
GetSigners defines whose signature is required

#### func (MsgFreezeCoins) Route

```go
func (msg MsgFreezeCoins) Route() string
```
Route should return the name of the module

#### func (MsgFreezeCoins) Type

```go
func (msg MsgFreezeCoins) Type() string
```
Type should return the action

#### func (MsgFreezeCoins) ValidateBasic

```go
func (msg MsgFreezeCoins) ValidateBasic() sdk.Error
```
ValidateBasic runs stateless checks on the message

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

#### func  NewMsgIssueToken

```go
func NewMsgIssueToken(sourceAddress, owner sdk.AccAddress, name, symbol string, originalSymbol string, maxSupply sdk.Int, mintable bool) MsgIssueToken
```
NewMsgIssueToken is a constructor function for MsgIssueToken

#### func (MsgIssueToken) GetSignBytes

```go
func (msg MsgIssueToken) GetSignBytes() []byte
```
GetSignBytes encodes the message for signing

#### func (MsgIssueToken) GetSigners

```go
func (msg MsgIssueToken) GetSigners() []sdk.AccAddress
```
GetSigners defines whose signature is required

#### func (MsgIssueToken) Route

```go
func (msg MsgIssueToken) Route() string
```
Route should return the name of the module

#### func (MsgIssueToken) Type

```go
func (msg MsgIssueToken) Type() string
```
Type should return the action

#### func (MsgIssueToken) ValidateBasic

```go
func (msg MsgIssueToken) ValidateBasic() sdk.Error
```
ValidateBasic runs stateless checks on the message

#### type MsgMintCoins

```go
type MsgMintCoins struct {
	Amount sdk.Int        `json:"amount" yaml:"amount"`
	Symbol string         `json:"symbol" yaml:"symbol"`
	Owner  sdk.AccAddress `json:"owner" yaml:"owner"`
}
```

MsgMintCoins defines the MintCoins message

#### func  NewMsgMintCoins

```go
func NewMsgMintCoins(amount sdk.Int, symbol string, owner sdk.AccAddress) MsgMintCoins
```
NewMsgMintCoins is the constructor function for MsgMintCoins

#### func (MsgMintCoins) GetSignBytes

```go
func (msg MsgMintCoins) GetSignBytes() []byte
```
GetSignBytes encodes the message for signing

#### func (MsgMintCoins) GetSigners

```go
func (msg MsgMintCoins) GetSigners() []sdk.AccAddress
```
GetSigners defines whose signature is required

#### func (MsgMintCoins) Route

```go
func (msg MsgMintCoins) Route() string
```
Route should return the name of the module

#### func (MsgMintCoins) Type

```go
func (msg MsgMintCoins) Type() string
```
Type should return the action

#### func (MsgMintCoins) ValidateBasic

```go
func (msg MsgMintCoins) ValidateBasic() sdk.Error
```
ValidateBasic runs stateless checks on the message

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

#### func  NewMsgUnfreezeCoins

```go
func NewMsgUnfreezeCoins(amount sdk.Int, symbol string, owner sdk.AccAddress, address sdk.AccAddress) MsgUnfreezeCoins
```
NewMsgUnfreezeCoins is the constructor function for MsgUnfreezeCoins

#### func (MsgUnfreezeCoins) GetSignBytes

```go
func (msg MsgUnfreezeCoins) GetSignBytes() []byte
```
GetSignBytes encodes the message for signing

#### func (MsgUnfreezeCoins) GetSigners

```go
func (msg MsgUnfreezeCoins) GetSigners() []sdk.AccAddress
```
GetSigners defines whose signature is required

#### func (MsgUnfreezeCoins) Route

```go
func (msg MsgUnfreezeCoins) Route() string
```
Route should return the name of the module

#### func (MsgUnfreezeCoins) Type

```go
func (msg MsgUnfreezeCoins) Type() string
```
Type should return the action

#### func (MsgUnfreezeCoins) ValidateBasic

```go
func (msg MsgUnfreezeCoins) ValidateBasic() sdk.Error
```
ValidateBasic runs stateless checks on the message

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
func NewParams(nominees []string) Params
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

#### type QueryResultSymbol

```go
type QueryResultSymbol []string
```

QueryResultSymbol is a payload for a symbols query

#### func (QueryResultSymbol) String

```go
func (r QueryResultSymbol) String() string
```
String implements fmt.Stringer

#### type Token

```go
type Token struct {
	Owner          sdk.AccAddress `json:"owner"`
	Name           string         `json:"name"`            // token name eg Fantom Chain Token
	Symbol         string         `json:"symbol"`          // unique token trade symbol eg FTM-000
	OriginalSymbol string         `json:"original_symbol"` // token symbol eg FTM
	MaxSupply      sdk.Int        `json:"max_supply"`      // Maximum mintable supply
	Mintable       bool           `json:"mintable"`
}
```

Token is a struct that contains all the metadata of the asset

#### func  NewToken

```go
func NewToken(name, symbol, originalSymbol string, maxSupply sdk.Int, owner sdk.AccAddress, mintable bool) *Token
```
NewToken returns a new token

#### func (Token) String

```go
func (t Token) String() string
```
String implements fmt.Stringer

#### func (Token) ValidateBasic

```go
func (t Token) ValidateBasic() sdk.Error
```
ValidateBasic does a simple validation check that doesn't require access to any
other information.
