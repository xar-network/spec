## Usage

```go
const (
	// ModuleKey is the name of the module
	ModuleName = "auction"
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
	// DefaultMaxAuctionDuration max length of auction, roughly 2 days in blocks
	DefaultMaxAuctionDuration EndTime = 2 * 24 * 3600 / 1
	// DefaultBidDuration how long an auction gets extended when someone bids, roughly 3 hours in blocks
	DefaultMaxBidDuration EndTime = 3 * 3600 / 1
	// DefaultStartingAuctionID what the id of the first auction will be
	DefaultStartingAuctionID ID = ID(1)
)
```
Defaults for auction params

```go
const (
	// QueryGetAuction command for getting the information about a particular auction
	QueryGetAuction = "getauctions"
)
```

```go
var (
	// ParamStoreKeyAuctionParams Param store key for auction params
	KeyAuctionBidDuration = []byte("MaxBidDuration")
	KeyAuctionDuration    = []byte("MaxAuctionDuration")
	KeyAuctionStartingID  = []byte("StartingAuctionID")
)
```
Parameter keys

```go
var ModuleCdc *codec.Codec
```
generic sealed codec to be used throughout module

#### func  NewForwardAuction

```go
func NewForwardAuction(seller sdk.AccAddress, lot sdk.Coin, initialBid sdk.Coin, endTime EndTime) (ForwardAuction, BankOutput)
```
NewForwardAuction creates a new forward auction

#### func  NewForwardReverseAuction

```go
func NewForwardReverseAuction(seller sdk.AccAddress, lot sdk.Coin, initialBid sdk.Coin, endTime EndTime, maxBid sdk.Coin, otherPerson sdk.AccAddress) (ForwardReverseAuction, BankOutput)
```
NewForwardReverseAuction creates a new forward reverse auction

#### func  NewReverseAuction

```go
func NewReverseAuction(buyer sdk.AccAddress, bid sdk.Coin, initialLot sdk.Coin, endTime EndTime) (ReverseAuction, BankOutput)
```
NewReverseAuction creates a new reverse auction

#### func  ParamKeyTable

```go
func ParamKeyTable() subspace.KeyTable
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
ValidateGenesis validates genesis inputs. Returns error if validation of any
input fails.

#### type Auction

```go
type Auction interface {
	GetID() ID
	SetID(ID)
	PlaceBid(currentBlockHeight EndTime, bidder sdk.AccAddress, lot sdk.Coin, bid sdk.Coin) ([]BankOutput, []BankInput, sdk.Error)
	GetEndTime() EndTime // auctions close at the end of the block with blockheight EndTime (ie bids placed in that block are valid)
	GetPayout() BankInput
	String() string
}
```

Auction is an interface to several types of auction.

#### type AuctionParams

```go
type AuctionParams struct {
	MaxAuctionDuration EndTime `json:"max_auction_duration" yaml:"max_auction_duration"` // max length of auction, in blocks
	MaxBidDuration     EndTime `json:"max_bid_duration" yaml:"max_bid_duration"`
	StartingAuctionID  ID      `json:"starting_auction_id" yaml:"starting_auction_id"`
}
```

AuctionParams governance parameters for auction module

#### func  DefaultAuctionParams

```go
func DefaultAuctionParams() AuctionParams
```
DefaultAuctionParams default parameters for auctions

#### func  NewAuctionParams

```go
func NewAuctionParams(maxAuctionDuration EndTime, bidDuration EndTime, startingID ID) AuctionParams
```
NewAuctionParams creates a new AuctionParams object

#### func (AuctionParams) Equal

```go
func (ap AuctionParams) Equal(ap2 AuctionParams) bool
```
Equal returns a boolean determining if two AuctionParams types are identical.

#### func (*AuctionParams) ParamSetPairs

```go
func (ap *AuctionParams) ParamSetPairs() subspace.ParamSetPairs
```
ParamSetPairs implements the ParamSet interface and returns all the key/value
pairs pairs of auth module's parameters. nolint

#### func (AuctionParams) String

```go
func (ap AuctionParams) String() string
```
String implements stringer interface

#### func (AuctionParams) Validate

```go
func (ap AuctionParams) Validate() error
```
Validate checks that the parameters have valid values.

#### type BankInput

```go
type BankInput struct {
	Address sdk.AccAddress
	Coin    sdk.Coin
}
```

Initially the input and output types from the bank module where used here. But
they use sdk.Coins instad of sdk.Coin. So it caused a lot of type conversion as
auction mainly uses sdk.Coin.

#### type BankOutput

```go
type BankOutput struct {
	Address sdk.AccAddress
	Coin    sdk.Coin
}
```


#### type BaseAuction

```go
type BaseAuction struct {
	ID         ID
	Initiator  sdk.AccAddress // Person who starts the auction. Giving away Lot (aka seller in a forward auction)
	Lot        sdk.Coin       // Amount of coins up being given by initiator (FA - amount for sale by seller, RA - cost of good by buyer (bid))
	Bidder     sdk.AccAddress // Person who bids in the auction. Receiver of Lot. (aka buyer in forward auction, seller in RA)
	Bid        sdk.Coin       // Amount of coins being given by the bidder (FA - bid, RA - amount being sold)
	EndTime    EndTime        // Block height at which the auction closes. It closes at the end of this block
	MaxEndTime EndTime        // Maximum closing time. Auctions can close before this but never after.
}
```

BaseAuction type shared by all Auctions

#### func  NewBaseAuction

```go
func NewBaseAuction(seller sdk.AccAddress, lot sdk.Coin, initialBid sdk.Coin, EndTime EndTime) BaseAuction
```
NewBaseAuction creates a new base auction

#### func (BaseAuction) GetEndTime

```go
func (a BaseAuction) GetEndTime() EndTime
```
GetEndTime getter for auction end time

#### func (BaseAuction) GetID

```go
func (a BaseAuction) GetID() ID
```
GetID getter for auction ID

#### func (BaseAuction) GetPayout

```go
func (a BaseAuction) GetPayout() BankInput
```
GetPayout implements Auction

#### func (*BaseAuction) SetID

```go
func (a *BaseAuction) SetID(id ID)
```
SetID setter for auction ID

#### func (BaseAuction) String

```go
func (a BaseAuction) String() string
```

#### type EndTime

```go
type EndTime int64 // TODO rename to Blockheight or don't define custom type

```


#### func (EndTime) String

```go
func (e EndTime) String() string
```

#### type ForwardAuction

```go
type ForwardAuction struct {
	BaseAuction
}
```

ForwardAuction type for forward auctions

#### func (*ForwardAuction) PlaceBid

```go
func (a *ForwardAuction) PlaceBid(currentBlockHeight EndTime, bidder sdk.AccAddress, lot sdk.Coin, bid sdk.Coin) ([]BankOutput, []BankInput, sdk.Error)
```
PlaceBid implements Auction

#### type ForwardReverseAuction

```go
type ForwardReverseAuction struct {
	BaseAuction
	MaxBid      sdk.Coin
	OtherPerson sdk.AccAddress // TODO rename, this is normally the original CSDT owner
}
```

ForwardReverseAuction type for forward reverse auction

#### func (*ForwardReverseAuction) PlaceBid

```go
func (a *ForwardReverseAuction) PlaceBid(currentBlockHeight EndTime, bidder sdk.AccAddress, lot sdk.Coin, bid sdk.Coin) (outputs []BankOutput, inputs []BankInput, err sdk.Error)
```
PlaceBid implements auction

#### func (ForwardReverseAuction) String

```go
func (a ForwardReverseAuction) String() string
```

#### type GenesisAuctions

```go
type GenesisAuctions []Auction
```

GenesisAuctions type for an array of auctions

#### type GenesisState

```go
type GenesisState struct {
	AuctionParams AuctionParams   `json:"auction_params" yaml:"auction_params"`
	Auctions      GenesisAuctions `json:"genesis_auctions" yaml:"genesis_auctions"`
}
```

GenesisState - auction state that must be provided at genesis

#### func  DefaultGenesisState

```go
func DefaultGenesisState() GenesisState
```
DefaultGenesisState defines default genesis state for auction module

#### func  NewGenesisState

```go
func NewGenesisState(ap AuctionParams, ga GenesisAuctions) GenesisState
```
NewGenesisState returns a new genesis state object for auctions module

#### func (GenesisState) Equal

```go
func (data GenesisState) Equal(data2 GenesisState) bool
```
Equal checks whether two GenesisState structs are equivalent

#### func (GenesisState) IsEmpty

```go
func (data GenesisState) IsEmpty() bool
```
IsEmpty returns true if a GenesisState is empty

#### type ID

```go
type ID uint64
```

ID type for auction IDs

#### func  NewIDFromString

```go
func NewIDFromString(s string) (ID, error)
```
NewIDFromString generate new auction ID from a string

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

#### func  NewMsgPlaceBid

```go
func NewMsgPlaceBid(auctionID ID, bidder sdk.AccAddress, bid sdk.Coin, lot sdk.Coin) MsgPlaceBid
```
NewMsgPlaceBid returns a new MsgPlaceBid.

#### func (MsgPlaceBid) GetSignBytes

```go
func (msg MsgPlaceBid) GetSignBytes() []byte
```
GetSignBytes gets the canonical byte representation of the Msg.

#### func (MsgPlaceBid) GetSigners

```go
func (msg MsgPlaceBid) GetSigners() []sdk.AccAddress
```
GetSigners returns the addresses of signers that must sign.

#### func (MsgPlaceBid) Route

```go
func (msg MsgPlaceBid) Route() string
```
Route return the message type used for routing the message.

#### func (MsgPlaceBid) Type

```go
func (msg MsgPlaceBid) Type() string
```
Type returns a human-readable string for the message, intended for utilization
within tags.

#### func (MsgPlaceBid) ValidateBasic

```go
func (msg MsgPlaceBid) ValidateBasic() sdk.Error
```
ValidateBasic does a simple validation check that doesn't require access to any
other information.

#### type QueryResAuctions

```go
type QueryResAuctions []string
```

QueryResAuctions Result Payload for an auctions query

#### func (QueryResAuctions) String

```go
func (n QueryResAuctions) String() string
```
implement fmt.Stringer

#### type ReverseAuction

```go
type ReverseAuction struct {
	BaseAuction
}
```

ReverseAuction type for reverse auctions

#### func (*ReverseAuction) PlaceBid

```go
func (a *ReverseAuction) PlaceBid(currentBlockHeight EndTime, bidder sdk.AccAddress, lot sdk.Coin, bid sdk.Coin) ([]BankOutput, []BankInput, sdk.Error)
```
PlaceBid implements Auction

#### type SupplyKeeper

```go
type SupplyKeeper interface {
	SendCoinsFromAccountToModule(ctx sdk.Context, senderAddr sdk.AccAddress, recipientModule string, amt sdk.Coins) sdk.Error
	SendCoinsFromModuleToAccount(ctx sdk.Context, senderModule string, recipientAddr sdk.AccAddress, amt sdk.Coins) sdk.Error
	//For Debt auctions
	MintCoins(ctx sdk.Context, moduleName string, amt sdk.Coins) sdk.Error
}
```
