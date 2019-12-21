# types
--
    import "github.com/xar-network/xar-network/x/uniswap/internal/types"


## Usage

```go
const (
	DefaultCodespace sdk.CodespaceType = ModuleName

	CodeReservePoolAlreadyExists    sdk.CodeType = 101
	CodeEqualDenom                  sdk.CodeType = 102
	CodeInvalidDeadline             sdk.CodeType = 103
	CodeNotPositive                 sdk.CodeType = 104
	CodeConstraintNotMet            sdk.CodeType = 105
	CodeNotSupported                sdk.CodeType = 106
	CodeCannotCreateReservePool     sdk.CodeType = 107
	CodeInvalidAccountAddr          sdk.CodeType = 108
	CodeInvalidAccountPemission     sdk.CodeType = 109
	CodeQueryParamIsInvalid         sdk.CodeType = 110
	CodeInsufficientLiquidityAmount sdk.CodeType = 111
	CodeReservePoolNotFound         sdk.CodeType = 111
)
```

```go
const (
	ReservePoolAlreadyExists         = "reserve pool already exists"
	EqualDenom                       = "input and output denomination are equal"
	InvalidDeadline                  = "invalid deadline"
	AmountIsNotPositive              = "amount is not positive"
	ConstraintNotMet                 = "constraint not met"
	NotCurrentlySupported            = "not currently supported"
	InvalidQueryParameter            = "query parameter is invalid"
	CannotCreateReservePool          = "cannot create reserve pool"
	InsufficientLiquidityAmount      = "insufficient liquidity amount"
	InsufficientCoins                = "sender does not have sufficient funds"
	LiquidityAddDeadLineHasPassed    = "deadline has passed for MsgAddLiquidity"
	LiquidityRemoveDeadLineHasPassed = "deadline has passed for MsgRemoveLiquidity"
)
```
constant set for error messages

```go
const (
	// ModuleName is the name of the module.
	ModuleName = "uniswap"

	// RouterKey is the message route for the uniswap module.
	RouterKey = ModuleName

	// StoreKey is the default store key for the uniswap module.
	StoreKey = ModuleName

	// QuerierRoute is the querier route for the uniswap module.
	QuerierRoute = StoreKey
)
```

```go
const (
	// Query endpoints supported by the coinswap querier
	QueryLiquidity  = "liquidity"
	QueryParameters = "parameters"

	ParamFee         = "fee"
	ParamNativeDenom = "nativeDenom"
)
```

```go
const (
	DefaultParamspace = ModuleName
)
```

```go
var (
	KeyNativeDenom = []byte("nativeDenom")
	KeyFee         = []byte("fee")
)
```
Parameter store keys

```go
var ModuleCdc *codec.Codec
```
ModuleCdc generic sealed codec to be used throughout module

#### func  ErrCannotCreateReservePool

```go
func ErrCannotCreateReservePool(codespace sdk.CodespaceType) sdk.Error
```

#### func  ErrConstraintNotMet

```go
func ErrConstraintNotMet(codespace sdk.CodespaceType, msg string) sdk.Error
```

#### func  ErrEqualDenom

```go
func ErrEqualDenom(codespace sdk.CodespaceType, msg string) sdk.Error
```

#### func  ErrInsufficientLiquidityAmount

```go
func ErrInsufficientLiquidityAmount(codespace sdk.CodespaceType) sdk.Error
```

#### func  ErrInvalidAccountAddr

```go
func ErrInvalidAccountAddr(codespace sdk.CodespaceType, msg string) sdk.Error
```

#### func  ErrInvalidAccountPermission

```go
func ErrInvalidAccountPermission(codespace sdk.CodespaceType, msg string) sdk.Error
```

#### func  ErrInvalidDeadline

```go
func ErrInvalidDeadline(codespace sdk.CodespaceType, msg string) sdk.Error
```

#### func  ErrNotPositive

```go
func ErrNotPositive(codespace sdk.CodespaceType, msg string) sdk.Error
```

#### func  ErrNotSupported

```go
func ErrNotSupported(codespace sdk.CodespaceType, msg string) sdk.Error
```

#### func  ErrQueryParamIsInvalid

```go
func ErrQueryParamIsInvalid(codespace sdk.CodespaceType, msg string) sdk.Error
```

#### func  ErrReservePoolAlreadyExists

```go
func ErrReservePoolAlreadyExists(codespace sdk.CodespaceType, msg string) sdk.Error
```

#### func  ErrReservePoolNotFound

```go
func ErrReservePoolNotFound(codespace sdk.CodespaceType, moduleName string) sdk.Error
```

#### func  MsgAccPermissionsError

```go
func MsgAccPermissionsError(moduleName string) string
```

#### func  MsgReservePoolNotFound

```go
func MsgReservePoolNotFound(moduleName string) string
```

#### func  ParamIsValid

```go
func ParamIsValid(p string) bool
```
return if parameter is present at the paramList

#### func  ParamKeyTable

```go
func ParamKeyTable() params.KeyTable
```
ParamKeyTable returns the KeyTable for coinswap module

#### func  RegisterCodec

```go
func RegisterCodec(cdc *codec.Codec)
```
RegisterCodec registers concrete types on the codec.

#### func  ValidateParams

```go
func ValidateParams(p Params) error
```
ValidateParams validates a set of params

#### type BankKeeper

```go
type BankKeeper interface {
	HasCoins(ctx sdk.Context, addr sdk.AccAddress, amt sdk.Coins) bool
	GetCoins(ctx sdk.Context, addr sdk.AccAddress) sdk.Coins
}
```

BankKeeper defines the expected bank keeper

#### type FeeParam

```go
type FeeParam struct {
	Numerator   sdk.Int `json:"fee_numerator"`
	Denominator sdk.Int `json:"fee_denominator"`
}
```

FeeParam defines the numerator and denominator used in calculating the amount to
be reserved as a liquidity fee. TODO: come up with a more descriptive name than
Numerator/Denominator Fee = 1 - (Numerator / Denominator) TODO: move this to
spec

#### func  NewFeeParam

```go
func NewFeeParam(numerator, denominator sdk.Int) FeeParam
```

#### func (FeeParam) String

```go
func (fp FeeParam) String() sdk.Dec
```
String returns a decimal representation of the parameters.

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

#### func  NewMsgAddLiquidity

```go
func NewMsgAddLiquidity(
	deposit sdk.Coin, depositAmount, minReward sdk.Int,
	deadline time.Time, sender sdk.AccAddress,
) MsgAddLiquidity
```
NewMsgAddLiquidity creates a new MsgAddLiquidity object.

#### func (MsgAddLiquidity) GetSignBytes

```go
func (msg MsgAddLiquidity) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgAddLiquidity) GetSigners

```go
func (msg MsgAddLiquidity) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgAddLiquidity) Route

```go
func (msg MsgAddLiquidity) Route() string
```
Type Implements Msg.

#### func (MsgAddLiquidity) Type

```go
func (msg MsgAddLiquidity) Type() string
```
Type Implements Msg.

#### func (MsgAddLiquidity) ValidateBasic

```go
func (msg MsgAddLiquidity) ValidateBasic() sdk.Error
```
ValidateBasic Implements Msg.

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

#### func  NewMsgRemoveLiquidity

```go
func NewMsgRemoveLiquidity(
	withdraw sdk.Coin, withdrawAmount, minNative sdk.Int,
	deadline time.Time, sender sdk.AccAddress,
) MsgRemoveLiquidity
```
NewMsgRemoveLiquidity creates a new MsgRemoveLiquidity object

#### func (MsgRemoveLiquidity) GetSignBytes

```go
func (msg MsgRemoveLiquidity) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgRemoveLiquidity) GetSigners

```go
func (msg MsgRemoveLiquidity) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgRemoveLiquidity) Route

```go
func (msg MsgRemoveLiquidity) Route() string
```
Type Implements Msg.

#### func (MsgRemoveLiquidity) Type

```go
func (msg MsgRemoveLiquidity) Type() string
```
Type Implements Msg.

#### func (MsgRemoveLiquidity) ValidateBasic

```go
func (msg MsgRemoveLiquidity) ValidateBasic() sdk.Error
```
ValidateBasic Implements Msg.

#### type MsgSwapOrder

```go
type MsgSwapOrder struct {
	Input     sdk.Coin       `json:"input"`    // the amount the sender is trading
	Output    sdk.Coin       `json:"output"`   // the amount the sender is recieivng
	Deadline  time.Time      `json:"deadline"` // deadline for the transaction to still be considered valid
	Sender    sdk.AccAddress `json:"sender"`
	Recipient sdk.AccAddress `json:"recipient"`
	// why do we realy need this var? let Input be always a value sender already has, and Output - a value recipient is seeking to obtain
	IsBuyOrder bool `json:"is_buy_order"` // boolean indicating whether the order should be treated as a buy or sell
}
```

MsgSwap Order - struct for swapping a coin Input and Output can either be exact
or calculated. An exact coin has the senders desired buy or sell amount. A
calculated coin has the desired denomination and bounded amount the sender is
willing to buy or sell in this order.

#### func  NewMsgSwapOrder

```go
func NewMsgSwapOrder(
	input, output sdk.Coin, deadline time.Time,
	sender, recipient sdk.AccAddress, isBuyOrder bool,
) MsgSwapOrder
```
NewMsgSwapOrder creates a new MsgSwapOrder object.

#### func (MsgSwapOrder) GetSignBytes

```go
func (msg MsgSwapOrder) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgSwapOrder) GetSigners

```go
func (msg MsgSwapOrder) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (*MsgSwapOrder) IsDoubleSwap

```go
func (msg *MsgSwapOrder) IsDoubleSwap(nativeDenom string) bool
```

#### func (MsgSwapOrder) Route

```go
func (msg MsgSwapOrder) Route() string
```
Route Implements Msg.

#### func (MsgSwapOrder) Type

```go
func (msg MsgSwapOrder) Type() string
```
Type Implements Msg.

#### func (MsgSwapOrder) ValidateBasic

```go
func (msg MsgSwapOrder) ValidateBasic() sdk.Error
```
ValidateBasic Implements Msg.

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


#### func (MsgTransactionOrder) GetSignBytes

```go
func (msg MsgTransactionOrder) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgTransactionOrder) GetSigners

```go
func (msg MsgTransactionOrder) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (*MsgTransactionOrder) IsDoubleSwap

```go
func (msg *MsgTransactionOrder) IsDoubleSwap(nativeDenom string) bool
```

#### func (MsgTransactionOrder) Route

```go
func (msg MsgTransactionOrder) Route() string
```
Route Implements Msg.

#### func (MsgTransactionOrder) Type

```go
func (msg MsgTransactionOrder) Type() string
```
Type Implements Msg.

#### func (MsgTransactionOrder) ValidateBasic

```go
func (msg MsgTransactionOrder) ValidateBasic() sdk.Error
```
ValidateBasic Implements Msg.

#### type Params

```go
type Params struct {
	NativeDenom string   `json:"native_denom"`
	Fee         FeeParam `json:"fee"`
}
```

Params defines the fee and native denomination for coinswap

#### func  DefaultParams

```go
func DefaultParams() Params
```
DefaultParams returns the default coinswap module parameters

#### func  NewParams

```go
func NewParams(nativeDenom string, fee FeeParam) Params
```

#### func (*Params) ParamSetPairs

```go
func (p *Params) ParamSetPairs() params.ParamSetPairs
```
Implements params.ParamSet.

#### func (Params) String

```go
func (p Params) String() string
```
String returns a human readable string representation of the parameters.

#### type QueryLiquidityParams

```go
type QueryLiquidityParams struct {
	NonNativeDenom string
}
```

defines the params for the following queries: - 'custom/coinswap/liquidity'

#### func  NewQueryLiquidityParams

```go
func NewQueryLiquidityParams(nonNativeDenom string) QueryLiquidityParams
```
Params used for querying liquidity

#### func (QueryLiquidityParams) String

```go
func (l QueryLiquidityParams) String() string
```

#### type SupplyKeeper

```go
type SupplyKeeper interface {
	GetModuleAccount(ctx sdk.Context, moduleName string) supply.ModuleAccountI
	SetModuleAccount(ctx sdk.Context, macc supply.ModuleAccountI)

	SendCoinsFromModuleToAccount(ctx sdk.Context, senderModule string, recipientAddr sdk.AccAddress, amt sdk.Coins) sdk.Error
	SendCoinsFromAccountToModule(ctx sdk.Context, senderAddr sdk.AccAddress, recipientModule string, amt sdk.Coins) sdk.Error

	MintCoins(ctx sdk.Context, moduleName string, amt sdk.Coins) sdk.Error
	BurnCoins(ctx sdk.Context, moduleName string, amt sdk.Coins) sdk.Error
}
```

SupplyKeeper defines the expected supply keeper
