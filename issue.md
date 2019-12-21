# types
--
    import "github.com/xar-network/xar-network/x/issue/internal/types"


## Usage

```go
const (
	DefaultCodespace sdk.CodespaceType = ModuleName

	CodeNotEnoughFee              sdk.CodeType = 3501
	CodeIssuerMismatch            sdk.CodeType = 3502
	CodeIssueIDNotValid           sdk.CodeType = 3503
	CodeIssueNameNotValid         sdk.CodeType = 3504
	CodeAmountNotValid            sdk.CodeType = 3505
	CodeIssueSymbolNotValid       sdk.CodeType = 3506
	CodeIssueTotalSupplyNotValid  sdk.CodeType = 3507
	CodeIssueDescriptionNotValid  sdk.CodeType = 3509
	CodeUnknownIssue              sdk.CodeType = 3510
	CanNotMint                    sdk.CodeType = 3511
	CanNotBurn                    sdk.CodeType = 3512
	CodeUnknownFeature            sdk.CodeType = 3513
	CodeUnknownFreezeType         sdk.CodeType = 3514
	CodeNotEnoughAmountToTransfer sdk.CodeType = 3515
	CodeCanNotFreeze              sdk.CodeType = 3516
	CodeFreezeEndTimeNotValid     sdk.CodeType = 3517
	CodeNotTransferIn             sdk.CodeType = 3518
	CodeNotTransferOut            sdk.CodeType = 3519
	CodeNegativeInflation         sdk.CodeType = 3520
)
```
Issue errors reserve 3500 ~ 3599.

```go
const (
	QueryParams    = "params"
	QueryIssues    = "list"
	QueryIssue     = "query"
	QueryAllowance = "allowance"
	QueryFreeze    = "freeze"
	QueryFreezes   = "freezes"
	QuerySearch    = "search"
	NativeDenom    = "ucsdt"
)
```

```go
const (
	// ModuleKey is the name of the module
	ModuleName = "issue"
	// StoreKey is the store key string for issue
	StoreKey = ModuleName
	// RouterKey is the message route for issue
	RouterKey = ModuleName
	// QuerierRoute is the querier route for issue
	QuerierRoute = ModuleName
	// Parameter store default namestore
	DefaultParamspace = ModuleName
)
```

```go
const (
	IDPreStr = "xar"
	Custom   = "custom"
)
```

```go
const (
	TypeMsgIssue                  = "issue"
	TypeMsgIssueMint              = "issue_mint"
	TypeMsgIssueBurnOwner         = "issue_burn_owner"
	TypeMsgIssueBurnHolder        = "issue_burn_holder"
	TypeMsgIssueBurnFrom          = "issue_burn_from"
	TypeMsgIssueDisableFeature    = "issue_disable_feature"
	TypeMsgIssueDescription       = "issue_description"
	TypeMsgIssueTransferOwnership = "issue_transfer_ownership"
	TypeMsgIssueApprove           = "issue_approve"
	TypeMsgIssueSendFrom          = "issue_send_from"
	TypeMsgIssueIncreaseApproval  = "issue_increase_approval"
	TypeMsgIssueDecreaseApproval  = "issue_decrease_approval"
	TypeMsgIssueFreeze            = "issue_freeze"
	TypeMsgIssueUnFreeze          = "issue_unfreeze"
)
```

```go
const (
	CodeInvalidGenesis       sdk.CodeType = 102
	CoinNameMinLength                     = 3
	CoinNameMaxLength                     = 32
	CoinSymbolMinLength                   = 2
	CoinSymbolMaxLength                   = 8
	CoinDescriptionMaxLength              = 1024
)
```

```go
const (
	FreezeIn       = "in"
	FreezeOut      = "out"
	FreezeInAndOut = "in-out"
)
```

```go
const (
	BurnOwner  = "burn-owner"
	BurnHolder = "burn-holder"
	BurnFrom   = "burn-from"
	Freeze     = "freeze"
	Minting    = "minting"
)
```

```go
const (
	Approve          = "approve"
	IncreaseApproval = "increaseApproval"
	DecreaseApproval = "decreaseApproval"
)
```

```go
var (
	TxCategory     = "issue"
	EventTypeIssue = "slash"

	Action          = "action"
	Category        = "category"
	Sender          = "sender"
	Owner           = "owner"
	Fee             = "fee"
	IssueID         = "issue-id"
	Feature         = "feature"
	Name            = "name"
	Symbol          = "symbol"
	TotalSupply     = "total-supply"
	MintingFinished = "minting-finished"
	FreezeType      = "freeze-type"

	AttributeValueCategory = ModuleName
)
```
Issue module event types

```go
var (
	CoinMaxTotalSupply, _        = sdk.NewIntFromString("1000000000000000000000000000000000000")
	CoinIssueMaxId        uint64 = 999999999999
	CoinIssueMinId        uint64 = 100000000000
)
```

```go
var (
	// key for constant fee parameter
	ParamStoreKeyIssueFee         = []byte("IssueFee")
	ParamStoreKeyMintFee          = []byte("MintFee")
	ParamStoreKeyFreezeFee        = []byte("FreezeFee")
	ParamStoreKeyUnFreezeFee      = []byte("UnfreezeFee")
	ParamStoreKeyBurnFee          = []byte("BurnFee")
	ParamStoreKeyBurnFromFee      = []byte("BurnFromFee")
	ParamStoreKeyTransferOwnerFee = []byte("TransferOwnerFee")
	ParamStoreKeyDescribeFee      = []byte("DescribeFee")
)
```

```go
var Features = map[string]int{BurnOwner: 1, BurnHolder: 1, BurnFrom: 1, Freeze: 1, Minting: 1}
```

```go
var FreezeTypes = map[string]int{FreezeIn: 1, FreezeOut: 1, FreezeInAndOut: 1}
```

```go
var ModuleCdc *codec.Codec
```
module codec

#### func  CheckIssueId

```go
func CheckIssueId(issueID string) sdk.Error
```

#### func  ErrAmountNotValid

```go
func ErrAmountNotValid() sdk.Error
```

#### func  ErrCanNotBurn

```go
func ErrCanNotBurn() sdk.Error
```

#### func  ErrCanNotFreeze

```go
func ErrCanNotFreeze() sdk.Error
```

#### func  ErrCanNotMint

```go
func ErrCanNotMint() sdk.Error
```

#### func  ErrCanNotTransferIn

```go
func ErrCanNotTransferIn() sdk.Error
```

#### func  ErrCanNotTransferOut

```go
func ErrCanNotTransferOut() sdk.Error
```

#### func  ErrCoinDescriptionMaxLengthNotValid

```go
func ErrCoinDescriptionMaxLengthNotValid() sdk.Error
```

#### func  ErrCoinDescriptionNotValid

```go
func ErrCoinDescriptionNotValid() sdk.Error
```

#### func  ErrCoinNamelNotValid

```go
func ErrCoinNamelNotValid() sdk.Error
```

#### func  ErrCoinSymbolNotValid

```go
func ErrCoinSymbolNotValid() sdk.Error
```

#### func  ErrCoinTotalSupplyMaxValueNotValid

```go
func ErrCoinTotalSupplyMaxValueNotValid() sdk.Error
```

#### func  ErrIssueID

```go
func ErrIssueID() sdk.Error
```

#### func  ErrNegativeInterest

```go
func ErrNegativeInterest() sdk.Error
```

#### func  ErrNotEnoughAmountToTransfer

```go
func ErrNotEnoughAmountToTransfer() sdk.Error
```

#### func  ErrNotEnoughFee

```go
func ErrNotEnoughFee() sdk.Error
```

#### func  ErrOwnerMismatch

```go
func ErrOwnerMismatch() sdk.Error
```
Error constructors

#### func  ErrUnknownFeatures

```go
func ErrUnknownFeatures() sdk.Error
```

#### func  ErrUnknownFreezeType

```go
func ErrUnknownFreezeType() sdk.Error
```

#### func  ErrUnknownIssue

```go
func ErrUnknownIssue() sdk.Error
```

#### func  Errorf

```go
func Errorf(err sdk.Error) error
```
convert sdk.Error to error

#### func  GetQueryIssueAllowancePath

```go
func GetQueryIssueAllowancePath(issueID string, owner sdk.AccAddress, spender sdk.AccAddress) string
```

#### func  GetQueryIssueFreezePath

```go
func GetQueryIssueFreezePath(issueID string, accAddress sdk.AccAddress) string
```

#### func  GetQueryIssueFreezesPath

```go
func GetQueryIssueFreezesPath(issueID string) string
```

#### func  GetQueryIssuePath

```go
func GetQueryIssuePath(issueID string) string
```

#### func  GetQueryIssueSearchPath

```go
func GetQueryIssueSearchPath(symbol string) string
```

#### func  GetQueryIssuesPath

```go
func GetQueryIssuesPath() string
```

#### func  GetQueryParamsPath

```go
func GetQueryParamsPath() string
```

#### func  GetRandomString

```go
func GetRandomString(l int) string
```

#### func  IsIssueId

```go
func IsIssueId(issueID string) bool
```

#### func  ParamKeyTable

```go
func ParamKeyTable() params.KeyTable
```
ParamKeyTable for auth module

#### func  RegisterCodec

```go
func RegisterCodec(cdc *codec.Codec)
```
Register concrete types on codec codec

#### func  ValidateParams

```go
func ValidateParams(params Params) error
```
validate params

#### type AccountKeeper

```go
type AccountKeeper interface {
	NewAccountWithAddress(ctx sdk.Context, addr sdk.AccAddress) exported.Account

	GetAccount(ctx sdk.Context, addr sdk.AccAddress) exported.Account
	GetAllAccounts(ctx sdk.Context) []exported.Account
	SetAccount(ctx sdk.Context, acc exported.Account)

	IterateAccounts(ctx sdk.Context, process func(exported.Account) bool)
}
```

AccountKeeper defines the account contract that must be fulfilled when creating
a x/bank keeper.

#### type Approval

```go
type Approval struct {
	Amount sdk.Int `json:"amount"`
}
```


#### func  NewApproval

```go
func NewApproval(amount sdk.Int) Approval
```

#### func (Approval) String

```go
func (ci Approval) String() string
```

#### type BankKeeper

```go
type BankKeeper interface {
	GetCoins(ctx sdk.Context, addr sdk.AccAddress) sdk.Coins
	SendCoins(ctx sdk.Context, fromAddr sdk.AccAddress, toAddr sdk.AccAddress, amt sdk.Coins) sdk.Error
}
```

expected bank keeper

#### type CoinIssueInfo

```go
type CoinIssueInfo struct {
	IssueId            string         `json:"issue_id"`
	Issuer             sdk.AccAddress `json:"issuer"`
	Owner              sdk.AccAddress `json:"owner"`
	IssueTime          int64          `json:"issue_time"`
	Name               string         `json:"name"`
	Symbol             string         `json:"symbol"`
	TotalSupply        sdk.Int        `json:"total_supply"`
	Description        string         `json:"description"`
	BurnOwnerDisabled  bool           `json:"burn_owner_disabled"`
	BurnHolderDisabled bool           `json:"burn_holder_disabled"`
	BurnFromDisabled   bool           `json:"burn_from_disabled"`
	FreezeDisabled     bool           `json:"freeze_disabled"`
	MintingFinished    bool           `json:"minting_finished"`
}
```

Coin Issue Info

#### func (CoinIssueInfo) GetDescription

```go
func (ci CoinIssueInfo) GetDescription() string
```

#### func (CoinIssueInfo) GetIssueId

```go
func (ci CoinIssueInfo) GetIssueId() string
```
nolint

#### func (CoinIssueInfo) GetIssueTime

```go
func (ci CoinIssueInfo) GetIssueTime() int64
```

#### func (CoinIssueInfo) GetIssuer

```go
func (ci CoinIssueInfo) GetIssuer() sdk.AccAddress
```

#### func (CoinIssueInfo) GetName

```go
func (ci CoinIssueInfo) GetName() string
```

#### func (CoinIssueInfo) GetOwner

```go
func (ci CoinIssueInfo) GetOwner() sdk.AccAddress
```

#### func (CoinIssueInfo) GetSymbol

```go
func (ci CoinIssueInfo) GetSymbol() string
```

#### func (CoinIssueInfo) GetTotalSupply

```go
func (ci CoinIssueInfo) GetTotalSupply() sdk.Int
```

#### func (CoinIssueInfo) IsBurnFromDisabled

```go
func (ci CoinIssueInfo) IsBurnFromDisabled() bool
```

#### func (CoinIssueInfo) IsBurnHolderDisabled

```go
func (ci CoinIssueInfo) IsBurnHolderDisabled() bool
```

#### func (CoinIssueInfo) IsBurnOwnerDisabled

```go
func (ci CoinIssueInfo) IsBurnOwnerDisabled() bool
```

#### func (CoinIssueInfo) IsFreezeDisabled

```go
func (ci CoinIssueInfo) IsFreezeDisabled() bool
```

#### func (CoinIssueInfo) IsMintingFinished

```go
func (ci CoinIssueInfo) IsMintingFinished() bool
```

#### func (CoinIssueInfo) SetBurnFromDisabled

```go
func (ci CoinIssueInfo) SetBurnFromDisabled(burnFromDisabled bool)
```

#### func (CoinIssueInfo) SetBurnHolderDisabled

```go
func (ci CoinIssueInfo) SetBurnHolderDisabled(burnFromDisabled bool)
```

#### func (CoinIssueInfo) SetBurnOwnerDisabled

```go
func (ci CoinIssueInfo) SetBurnOwnerDisabled(burnOwnerDisabled bool)
```

#### func (*CoinIssueInfo) SetDescription

```go
func (ci *CoinIssueInfo) SetDescription(description string)
```

#### func (CoinIssueInfo) SetFreezeDisabled

```go
func (ci CoinIssueInfo) SetFreezeDisabled(freezeDisabled bool)
```

#### func (*CoinIssueInfo) SetIssueId

```go
func (ci *CoinIssueInfo) SetIssueId(issueId string)
```

#### func (*CoinIssueInfo) SetIssueTime

```go
func (ci *CoinIssueInfo) SetIssueTime(issueTime int64)
```

#### func (*CoinIssueInfo) SetIssuer

```go
func (ci *CoinIssueInfo) SetIssuer(issuer sdk.AccAddress)
```

#### func (CoinIssueInfo) SetMintingFinished

```go
func (ci CoinIssueInfo) SetMintingFinished(mintingFinished bool)
```

#### func (*CoinIssueInfo) SetName

```go
func (ci *CoinIssueInfo) SetName(name string)
```

#### func (*CoinIssueInfo) SetOwner

```go
func (ci *CoinIssueInfo) SetOwner(owner sdk.AccAddress)
```

#### func (*CoinIssueInfo) SetSymbol

```go
func (ci *CoinIssueInfo) SetSymbol(symbol string)
```

#### func (*CoinIssueInfo) SetTotalSupply

```go
func (ci *CoinIssueInfo) SetTotalSupply(totalSupply sdk.Int)
```

#### func (CoinIssueInfo) String

```go
func (ci CoinIssueInfo) String() string
```
nolint

#### type CoinIssues

```go
type CoinIssues []CoinIssueInfo
```

CoinIssues is an array of Issue

#### func (CoinIssues) String

```go
func (coinIssues CoinIssues) String() string
```
nolint

#### type Issue

```go
type Issue interface {
	GetIssueId() string
	SetIssueId(string)

	GetIssuer() sdk.AccAddress
	SetIssuer(sdk.AccAddress)

	GetOwner() sdk.AccAddress
	SetOwner(sdk.AccAddress)

	GetIssueTime() int64
	SetIssueTime(int64)

	GetName() string
	SetName(string)

	GetTotalSupply() sdk.Int
	SetTotalSupply(sdk.Int)

	GetDescription() string
	SetDescription(string)

	IsBurnOwnerDisabled() bool
	SetBurnOwnerDisabled(bool)

	IsBurnHolderDisabled() bool
	SetBurnHolderDisabled(bool)

	IsBurnFromDisabled() bool
	SetBurnFromDisabled(bool)

	IsFreezeDisabled() bool
	SetFreezeDisabled(bool)

	IsMintingFinished() bool
	SetMintingFinished(bool)

	GetSymbol() string
	SetSymbol(string)

	String() string
}
```

Issue interface

#### func  IssueOwnerCheck

```go
func IssueOwnerCheck(cliCtx context.CLIContext, sender sdk.AccAddress, issueID string) (Issue, error)
```

#### type IssueAddressFreeze

```go
type IssueAddressFreeze struct {
	Address string `json:"address"`
}
```


#### func (IssueAddressFreeze) String

```go
func (ci IssueAddressFreeze) String() string
```

#### type IssueAddressFreezeList

```go
type IssueAddressFreezeList []IssueAddressFreeze
```


#### func (IssueAddressFreezeList) String

```go
func (ci IssueAddressFreezeList) String() string
```
nolint

#### type IssueFreeze

```go
type IssueFreeze struct {
	Frozen bool `json:"frozen"`
}
```


#### func (IssueFreeze) String

```go
func (ci IssueFreeze) String() string
```

#### type IssueParams

```go
type IssueParams struct {
	Name               string  `json:"name"`
	Symbol             string  `json:"symbol"`
	TotalSupply        sdk.Int `json:"total_supply"`
	Description        string  `json:"description"`
	BurnOwnerDisabled  bool    `json:"burn_owner_disabled"`
	BurnHolderDisabled bool    `json:"burn_holder_disabled"`
	BurnFromDisabled   bool    `json:"burn_from_disabled"`
	MintingFinished    bool    `json:"minting_finished"`
	FreezeDisabled     bool    `json:"freeze_disabled"`
}
```

Param issue for issue

#### type IssueQueryParams

```go
type IssueQueryParams struct {
	StartIssueId string         `json:"start_issue_id"`
	Owner        sdk.AccAddress `json:"owner"`
	Limit        int            `json:"limit"`
}
```

Param query issue for issue

#### type MsgFlag

```go
type MsgFlag interface {
	sdk.Msg

	GetIssueId() string
	SetIssueId(string)

	GetSender() sdk.AccAddress
	SetSender(sdk.AccAddress)
}
```


#### type MsgIssue

```go
type MsgIssue struct {
	FromAddress  sdk.AccAddress `json:"from_address" yaml:"from_address"`
	*IssueParams `json:"params" yaml:"params"`
}
```

MsgIssue to allow a registered issuer to issue new coins.

#### func  NewMsgIssue

```go
func NewMsgIssue(fromAddr sdk.AccAddress, params *IssueParams) MsgIssue
```
NewMsgIssue Instance

#### func (MsgIssue) GetSignBytes

```go
func (msg MsgIssue) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgIssue) GetSigners

```go
func (msg MsgIssue) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgIssue) Route

```go
func (msg MsgIssue) Route() string
```
Route Implements Msg.

#### func (MsgIssue) Type

```go
func (msg MsgIssue) Type() string
```
Type Implements Msg.

#### func (MsgIssue) ValidateBasic

```go
func (msg MsgIssue) ValidateBasic() sdk.Error
```
ValidateBasic ensures addresses are valid and Coin is positive

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

#### func  NewMsgIssueApprove

```go
func NewMsgIssueApprove(
	issueId string,
	fromAddr, toAddr sdk.AccAddress,
	amount sdk.Int,
) MsgIssueApprove
```
New MsgIssueApprove Instance

#### func (MsgIssueApprove) GetSignBytes

```go
func (msg MsgIssueApprove) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgIssueApprove) GetSigners

```go
func (msg MsgIssueApprove) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgIssueApprove) Route

```go
func (msg MsgIssueApprove) Route() string
```
Route Implements Msg.

#### func (MsgIssueApprove) Type

```go
func (msg MsgIssueApprove) Type() string
```
Type Implements Msg.

#### func (MsgIssueApprove) ValidateBasic

```go
func (msg MsgIssueApprove) ValidateBasic() sdk.Error
```
Implements Msg. Ensures addresses are valid and Coin is positive

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

#### func  NewMsgIssueBurnFrom

```go
func NewMsgIssueBurnFrom(issueId string,
	fromAddr, toAddr sdk.AccAddress,
	amount sdk.Int,
) MsgIssueBurnFrom
```
New NewMsgIssueBurnFrom Instance

#### func (MsgIssueBurnFrom) GetSignBytes

```go
func (msg MsgIssueBurnFrom) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgIssueBurnFrom) GetSigners

```go
func (msg MsgIssueBurnFrom) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgIssueBurnFrom) Route

```go
func (msg MsgIssueBurnFrom) Route() string
```
Route Implements Msg.

#### func (MsgIssueBurnFrom) Type

```go
func (msg MsgIssueBurnFrom) Type() string
```
Type Implements Msg.

#### func (MsgIssueBurnFrom) ValidateBasic

```go
func (msg MsgIssueBurnFrom) ValidateBasic() sdk.Error
```
Implements Msg. Ensures addresses are valid and Coin is positive

#### type MsgIssueBurnHolder

```go
type MsgIssueBurnHolder struct {
	IssueId     string         `json:"issue_id" yaml:"issue_id"`
	FromAddress sdk.AccAddress `json:"from_address" yaml:"from_address"`
	Amount      sdk.Int        `json:"amount" yaml:"amount"`
}
```

MsgIssueBurnHolder to allow a registered owner

#### func  NewMsgIssueBurnHolder

```go
func NewMsgIssueBurnHolder(
	issueId string,
	fromAddr sdk.AccAddress,
	amount sdk.Int,
) MsgIssueBurnHolder
```
New NewMsgIssueBurnHolder Instance

#### func (MsgIssueBurnHolder) GetSignBytes

```go
func (msg MsgIssueBurnHolder) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgIssueBurnHolder) GetSigners

```go
func (msg MsgIssueBurnHolder) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgIssueBurnHolder) Route

```go
func (msg MsgIssueBurnHolder) Route() string
```
Route Implements Msg.

#### func (MsgIssueBurnHolder) Type

```go
func (msg MsgIssueBurnHolder) Type() string
```
Type Implements Msg.

#### func (MsgIssueBurnHolder) ValidateBasic

```go
func (msg MsgIssueBurnHolder) ValidateBasic() sdk.Error
```
Implements Msg. Ensures addresses are valid and Coin is positive

#### type MsgIssueBurnOwner

```go
type MsgIssueBurnOwner struct {
	IssueId     string         `json:"issue_id" yaml:"issue_id"`
	FromAddress sdk.AccAddress `json:"from_address" yaml:"from_address"`
	Amount      sdk.Int        `json:"amount" yaml:"amount"`
}
```

MsgIssueBurnOwner to allow a registered owner

#### func  NewMsgIssueBurnOwner

```go
func NewMsgIssueBurnOwner(
	issueId string,
	fromAddr sdk.AccAddress,
	amount sdk.Int,
) MsgIssueBurnOwner
```
New MsgIssueBurnOwner Instance

#### func (MsgIssueBurnOwner) GetSignBytes

```go
func (msg MsgIssueBurnOwner) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgIssueBurnOwner) GetSigners

```go
func (msg MsgIssueBurnOwner) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgIssueBurnOwner) Route

```go
func (msg MsgIssueBurnOwner) Route() string
```
Route Implements Msg.

#### func (MsgIssueBurnOwner) Type

```go
func (msg MsgIssueBurnOwner) Type() string
```
Type Implements Msg.

#### func (MsgIssueBurnOwner) ValidateBasic

```go
func (msg MsgIssueBurnOwner) ValidateBasic() sdk.Error
```
Implements Msg. Ensures addresses are valid and Coin is positive

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

#### func  NewMsgIssueDecreaseApproval

```go
func NewMsgIssueDecreaseApproval(
	issueId string,
	fromAddr, toAddr sdk.AccAddress,
	amount sdk.Int,
) MsgIssueDecreaseApproval
```
New MsgIssueDecreaseApproval Instance

#### func (MsgIssueDecreaseApproval) GetSignBytes

```go
func (msg MsgIssueDecreaseApproval) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgIssueDecreaseApproval) GetSigners

```go
func (msg MsgIssueDecreaseApproval) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgIssueDecreaseApproval) Route

```go
func (msg MsgIssueDecreaseApproval) Route() string
```
Route Implements Msg.

#### func (MsgIssueDecreaseApproval) Type

```go
func (msg MsgIssueDecreaseApproval) Type() string
```
Type Implements Msg.

#### func (MsgIssueDecreaseApproval) ValidateBasic

```go
func (msg MsgIssueDecreaseApproval) ValidateBasic() sdk.Error
```
Implements Msg. Ensures addresses are valid and Coin is positive

#### type MsgIssueDescription

```go
type MsgIssueDescription struct {
	IssueId     string         `json:"issue_id" yaml:"issue_id"`
	FromAddress sdk.AccAddress `json:"from_address" yaml:"from_address"`
	Description []byte         `json:"description" yaml:"description"`
}
```

MsgIssueDescription to allow a registered owner to issue new coins.

#### func  NewMsgIssueDescription

```go
func NewMsgIssueDescription(
	issueId string,
	fromAddr sdk.AccAddress,
	description []byte,
) MsgIssueDescription
```
New MsgIssueDescription Instance

#### func (MsgIssueDescription) GetSignBytes

```go
func (msg MsgIssueDescription) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgIssueDescription) GetSigners

```go
func (msg MsgIssueDescription) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgIssueDescription) Route

```go
func (msg MsgIssueDescription) Route() string
```
Route Implements Msg.

#### func (MsgIssueDescription) Type

```go
func (msg MsgIssueDescription) Type() string
```
Type Implements Msg.

#### func (MsgIssueDescription) ValidateBasic

```go
func (msg MsgIssueDescription) ValidateBasic() sdk.Error
```
Implements Msg. Ensures addresses are valid and Coin is positive

#### type MsgIssueDisableFeature

```go
type MsgIssueDisableFeature struct {
	IssueId     string         `json:"issue_id" yaml:"issue_id"`
	FromAddress sdk.AccAddress `json:"from_address" yaml:"from_address"`
	Feature     string         `json:"feature" yaml:"feature"`
}
```

MsgIssueDisableFeature to allow a registered owner

#### func  NewMsgIssueDisableFeature

```go
func NewMsgIssueDisableFeature(
	issueId string,
	fromAddr sdk.AccAddress,
	feature string,
) MsgIssueDisableFeature
```
New MsgIssueDisableFeature Instance

#### func (MsgIssueDisableFeature) GetSignBytes

```go
func (msg MsgIssueDisableFeature) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgIssueDisableFeature) GetSigners

```go
func (msg MsgIssueDisableFeature) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgIssueDisableFeature) Route

```go
func (msg MsgIssueDisableFeature) Route() string
```
Route Implements Msg.

#### func (MsgIssueDisableFeature) Type

```go
func (msg MsgIssueDisableFeature) Type() string
```
Type Implements Msg.

#### func (MsgIssueDisableFeature) ValidateBasic

```go
func (msg MsgIssueDisableFeature) ValidateBasic() sdk.Error
```
Implements Msg. Ensures addresses are valid and Coin is positive

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

#### func  NewMsgIssueFreeze

```go
func NewMsgIssueFreeze(
	issueId string,
	fromAddr,
	toAddr sdk.AccAddress,
	freezeType string,
) MsgIssueFreeze
```
New MsgIssueFreeze Instance

#### func (MsgIssueFreeze) GetSignBytes

```go
func (msg MsgIssueFreeze) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgIssueFreeze) GetSigners

```go
func (msg MsgIssueFreeze) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgIssueFreeze) Route

```go
func (msg MsgIssueFreeze) Route() string
```
Route Implements Msg.

#### func (MsgIssueFreeze) Type

```go
func (msg MsgIssueFreeze) Type() string
```
Type Implements Msg.

#### func (MsgIssueFreeze) ValidateBasic

```go
func (msg MsgIssueFreeze) ValidateBasic() sdk.Error
```
Implements Msg. Ensures addresses are valid and Coin is positive

#### func (MsgIssueFreeze) ValidateService

```go
func (msg MsgIssueFreeze) ValidateService() sdk.Error
```

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

#### func  NewMsgIssueIncreaseApproval

```go
func NewMsgIssueIncreaseApproval(
	issueId string,
	fromAddr,
	toAddr sdk.AccAddress,
	amount sdk.Int,
) MsgIssueIncreaseApproval
```
New MsgIssueIncreaseApproval Instance

#### func (MsgIssueIncreaseApproval) GetSignBytes

```go
func (msg MsgIssueIncreaseApproval) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgIssueIncreaseApproval) GetSigners

```go
func (msg MsgIssueIncreaseApproval) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgIssueIncreaseApproval) Route

```go
func (msg MsgIssueIncreaseApproval) Route() string
```
Route Implements Msg.

#### func (MsgIssueIncreaseApproval) Type

```go
func (msg MsgIssueIncreaseApproval) Type() string
```
Type Implements Msg.

#### func (MsgIssueIncreaseApproval) ValidateBasic

```go
func (msg MsgIssueIncreaseApproval) ValidateBasic() sdk.Error
```
Implements Msg. Ensures addresses are valid and Coin is positive

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

#### func  NewMsgIssueMint

```go
func NewMsgIssueMint(
	issueId string,
	fromAddr,
	toAddr sdk.AccAddress,
	amount sdk.Int,
) MsgIssueMint
```
NewMsgIssueMint Instance

#### func (MsgIssueMint) GetSignBytes

```go
func (msg MsgIssueMint) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgIssueMint) GetSigners

```go
func (msg MsgIssueMint) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgIssueMint) Route

```go
func (msg MsgIssueMint) Route() string
```
Route Implements Msg.

#### func (MsgIssueMint) Type

```go
func (msg MsgIssueMint) Type() string
```
Type Implements Msg.

#### func (MsgIssueMint) ValidateBasic

```go
func (msg MsgIssueMint) ValidateBasic() sdk.Error
```
Implements Msg. Ensures addresses are valid and Coin is positive

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

#### func  NewMsgIssueSendFrom

```go
func NewMsgIssueSendFrom(issueId string, fromAddr, from, toAddr sdk.AccAddress, amount sdk.Int) MsgIssueSendFrom
```
New MsgIssueSendFrom Instance

#### func (MsgIssueSendFrom) GetSignBytes

```go
func (msg MsgIssueSendFrom) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgIssueSendFrom) GetSigners

```go
func (msg MsgIssueSendFrom) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgIssueSendFrom) Route

```go
func (msg MsgIssueSendFrom) Route() string
```
Route Implements Msg.

#### func (MsgIssueSendFrom) Type

```go
func (msg MsgIssueSendFrom) Type() string
```
Type Implements Msg.

#### func (MsgIssueSendFrom) ValidateBasic

```go
func (msg MsgIssueSendFrom) ValidateBasic() sdk.Error
```
Implements Msg. Ensures addresses are valid and Coin is positive

#### type MsgIssueTransferOwnership

```go
type MsgIssueTransferOwnership struct {
	IssueId     string         `json:"issue_id" yaml:"issue_id"`
	FromAddress sdk.AccAddress `json:"from_address" yaml:"from_address"`
	ToAddress   sdk.AccAddress `json:"to_address" yaml:"to_address"`
}
```

MsgIssueTransferOwnership to allow a registered owner to issue new coins.

#### func  NewMsgIssueTransferOwnership

```go
func NewMsgIssueTransferOwnership(issueId string, fromAddr, toAddr sdk.AccAddress) MsgIssueTransferOwnership
```
New MsgIssueTransferOwnership Instance

#### func (MsgIssueTransferOwnership) GetSignBytes

```go
func (msg MsgIssueTransferOwnership) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgIssueTransferOwnership) GetSigners

```go
func (msg MsgIssueTransferOwnership) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgIssueTransferOwnership) Route

```go
func (msg MsgIssueTransferOwnership) Route() string
```
Route Implements Msg.

#### func (MsgIssueTransferOwnership) Type

```go
func (msg MsgIssueTransferOwnership) Type() string
```
Type Implements Msg.

#### func (MsgIssueTransferOwnership) ValidateBasic

```go
func (msg MsgIssueTransferOwnership) ValidateBasic() sdk.Error
```
Implements Msg. Ensures addresses are valid and Coin is positive

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

#### func  NewMsgIssueUnFreeze

```go
func NewMsgIssueUnFreeze(issueId string, fromAddr, toAddr sdk.AccAddress, freezeType string) MsgIssueUnFreeze
```
New MsgIssueUnFreeze Instance

#### func (MsgIssueUnFreeze) GetSignBytes

```go
func (msg MsgIssueUnFreeze) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgIssueUnFreeze) GetSigners

```go
func (msg MsgIssueUnFreeze) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgIssueUnFreeze) Route

```go
func (msg MsgIssueUnFreeze) Route() string
```
Route Implements Msg.

#### func (MsgIssueUnFreeze) Type

```go
func (msg MsgIssueUnFreeze) Type() string
```
Type Implements Msg.

#### func (MsgIssueUnFreeze) ValidateBasic

```go
func (msg MsgIssueUnFreeze) ValidateBasic() sdk.Error
```
Implements Msg. Ensures addresses are valid and Coin is positive

#### type MsgSetInterest

```go
type MsgSetInterest struct {
	Denom        string
	InterestRate sdk.Dec
	Issuer       sdk.AccAddress
}
```


#### func (MsgSetInterest) GetSignBytes

```go
func (msg MsgSetInterest) GetSignBytes() []byte
```

#### func (MsgSetInterest) GetSigners

```go
func (msg MsgSetInterest) GetSigners() []sdk.AccAddress
```

#### func (MsgSetInterest) Route

```go
func (msg MsgSetInterest) Route() string
```

#### func (MsgSetInterest) Type

```go
func (msg MsgSetInterest) Type() string
```

#### func (MsgSetInterest) ValidateBasic

```go
func (msg MsgSetInterest) ValidateBasic() sdk.Error
```

#### type Params

```go
type Params struct {
	IssueFee         sdk.Coin `json:"issue_fee"`
	MintFee          sdk.Coin `json:"mint_fee"`
	FreezeFee        sdk.Coin `json:"freeze_fee"`
	UnFreezeFee      sdk.Coin `json:"unfreeze_fee"`
	BurnFee          sdk.Coin `json:"burn_fee"`
	BurnFromFee      sdk.Coin `json:"burn_from_fee"`
	TransferOwnerFee sdk.Coin `json:"transfer_owner_fee"`
	DescribeFee      sdk.Coin `json:"describe_fee"`
}
```

Param Config issue for issue

#### func  DefaultParams

```go
func DefaultParams(denom string) Params
```
DefaultParams returns a default set of parameters.

#### func (Params) Equal

```go
func (dp Params) Equal(dp2 Params) bool
```
Checks equality of Params

#### func (*Params) ParamSetPairs

```go
func (p *Params) ParamSetPairs() params.ParamSetPairs
```
ParamSetPairs implements the ParamSet interface and returns all the key/value
pairs pairs of auth module's parameters. nolint

#### func (Params) String

```go
func (dp Params) String() string
```

#### type SupplyKeeper

```go
type SupplyKeeper interface {
	SendCoinsFromAccountToModule(ctx sdk.Context, senderAddr sdk.AccAddress, recipientModule string, amt sdk.Coins) sdk.Error
	SendCoinsFromModuleToAccount(ctx sdk.Context, senderModule string, recipientAddr sdk.AccAddress, amt sdk.Coins) sdk.Error
	BurnCoins(ctx sdk.Context, moduleName string, amt sdk.Coins) sdk.Error
	MintCoins(ctx sdk.Context, moduleName string, amt sdk.Coins) sdk.Error
	SetSupply(ctx sdk.Context, supply supply.SupplyI)
}
```

expected supply keeper
