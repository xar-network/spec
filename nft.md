# nft
--
    import "github.com/xar-network/xar-network/x/nft/internal/types"


## Usage

```go
const (
	// ModuleName is the name of the module
	ModuleName = "nft"

	// StoreKey is the default store key for NFT
	StoreKey = ModuleName

	// QuerierRoute is the querier route for the NFT store.
	QuerierRoute = ModuleName

	// RouterKey is the message route for the NFT module
	RouterKey = ModuleName
)
```

```go
var (
	EventTypeTransfer        = "transfer_nft"
	EventTypeEditNFTMetadata = "edit_nft_metadata"
	EventTypeMintNFT         = "mint_nft"
	EventTypeBurnNFT         = "burn_nft"

	AttributeValueCategory = ModuleName

	AttributeKeySender      = "sender"
	AttributeKeyRecipient   = "recipient"
	AttributeKeyOwner       = "owner"
	AttributeKeyNFTID       = "nft-id"
	AttributeKeyNFTTokenURI = "token-uri"
	AttributeKeyDenom       = "denom"
)
```
NFT module event types

```go
var (
	CollectionsKeyPrefix = []byte{0x00} // key for NFT collections
	OwnersKeyPrefix      = []byte{0x01} // key for balance of NFTs held by an address
)
```
NFTs are stored as follow:

- Colections: 0x00<denom_bytes_key> :<Collection>

- Owners: 0x01<address_bytes_key><denom_bytes_key>: <Owner>

```go
var ModuleCdc *codec.Codec
```
ModuleCdc generic sealed codec to be used throughout this module

#### func  CreateTestAddrs

```go
func CreateTestAddrs(numAddrs int) []sdk.AccAddress
```
CreateTestAddrs creates test addresses

#### func  ErrEmptyMetadata

```go
func ErrEmptyMetadata(codespace sdk.CodespaceType, msg string) sdk.Error
```
ErrEmptyMetadata is an error when metadata is empty

#### func  ErrInvalidCollection

```go
func ErrInvalidCollection(codespace sdk.CodespaceType) sdk.Error
```
ErrInvalidCollection is an error

#### func  ErrInvalidNFT

```go
func ErrInvalidNFT(codespace sdk.CodespaceType) sdk.Error
```
ErrInvalidNFT is an error

#### func  ErrNFTAlreadyExists

```go
func ErrNFTAlreadyExists(codespace sdk.CodespaceType, msg string) sdk.Error
```
ErrNFTAlreadyExists is an error when an invalid NFT is minted

#### func  ErrUnknownCollection

```go
func ErrUnknownCollection(codespace sdk.CodespaceType, msg string) sdk.Error
```
ErrUnknownCollection is an error

#### func  ErrUnknownNFT

```go
func ErrUnknownNFT(codespace sdk.CodespaceType, msg string) sdk.Error
```
ErrUnknownNFT is an error

#### func  FindUtil

```go
func FindUtil(group Findable, el string) int
```
FindUtil is a binary search funcion for types that support the Findable
interface (elements must be sorted)

#### func  GetCollectionKey

```go
func GetCollectionKey(denom string) []byte
```
GetCollectionKey gets the key of a collection

#### func  GetOwnerKey

```go
func GetOwnerKey(address sdk.AccAddress, denom string) []byte
```
GetOwnerKey gets the key of a collection owned by an account address

#### func  GetOwnersKey

```go
func GetOwnersKey(address sdk.AccAddress) []byte
```
GetOwnersKey gets the key prefix for all the collections owned by an account
address

#### func  RegisterCodec

```go
func RegisterCodec(cdc *codec.Codec)
```
RegisterCodec concrete types on codec

#### func  SplitOwnerKey

```go
func SplitOwnerKey(key []byte) (sdk.AccAddress, []byte)
```
SplitOwnerKey gets an address and denom from an owner key

#### func  ValidateGenesis

```go
func ValidateGenesis(data GenesisState) error
```
ValidateGenesis performs basic validation of nfts genesis data returning an
error for any failed validation criteria.

#### type BaseNFT

```go
type BaseNFT struct {
	ID       string         `json:"id,omitempty" yaml:"id"`     // id of the token; not exported to clients
	Owner    sdk.AccAddress `json:"owner" yaml:"owner"`         // account address that owns the NFT
	TokenURI string         `json:"token_uri" yaml:"token_uri"` // optional extra properties available for querying
}
```

BaseNFT non fungible token definition

#### func  NewBaseNFT

```go
func NewBaseNFT(id string, owner sdk.AccAddress, tokenURI string) BaseNFT
```
NewBaseNFT creates a new NFT instance

#### func (*BaseNFT) EditMetadata

```go
func (bnft *BaseNFT) EditMetadata(tokenURI string)
```
EditMetadata edits metadata of an nft

#### func (BaseNFT) GetID

```go
func (bnft BaseNFT) GetID() string
```
GetID returns the ID of the token

#### func (BaseNFT) GetOwner

```go
func (bnft BaseNFT) GetOwner() sdk.AccAddress
```
GetOwner returns the account address that owns the NFT

#### func (BaseNFT) GetTokenURI

```go
func (bnft BaseNFT) GetTokenURI() string
```
GetTokenURI returns the path to optional extra properties

#### func (*BaseNFT) SetOwner

```go
func (bnft *BaseNFT) SetOwner(address sdk.AccAddress)
```
SetOwner updates the owner address of the NFT

#### func (BaseNFT) String

```go
func (bnft BaseNFT) String() string
```

#### type CodeType

```go
type CodeType = sdk.CodeType
```

CodeType definition

```go
const (
	DefaultCodespace sdk.CodespaceType = ModuleName

	CodeInvalidCollection CodeType = 650
	CodeUnknownCollection CodeType = 651
	CodeInvalidNFT        CodeType = 652
	CodeUnknownNFT        CodeType = 653
	CodeNFTAlreadyExists  CodeType = 654
	CodeEmptyMetadata     CodeType = 655
)
```
NFT error code

#### type Collection

```go
type Collection struct {
	Denom string `json:"denom,omitempty" yaml:"denom"` // name of the collection; not exported to clients
	NFTs  NFTs   `json:"nfts" yaml:"nfts"`             // NFTs that belong to a collection
}
```

Collection of non fungible tokens

#### func  EmptyCollection

```go
func EmptyCollection() Collection
```
EmptyCollection returns an empty collection

#### func  NewCollection

```go
func NewCollection(denom string, nfts NFTs) Collection
```
NewCollection creates a new NFT Collection

#### func (Collection) AddNFT

```go
func (collection Collection) AddNFT(nft exported.NFT) (Collection, sdk.Error)
```
AddNFT adds an NFT to the collection

#### func (Collection) ContainsNFT

```go
func (collection Collection) ContainsNFT(id string) bool
```
ContainsNFT returns whether or not a Collection contains an NFT

#### func (Collection) DeleteNFT

```go
func (collection Collection) DeleteNFT(nft exported.NFT) (Collection, sdk.Error)
```
DeleteNFT deletes an NFT from a collection

#### func (Collection) GetNFT

```go
func (collection Collection) GetNFT(id string) (nft exported.NFT, err sdk.Error)
```
GetNFT gets a NFT from the collection

#### func (Collection) String

```go
func (collection Collection) String() string
```
String follows stringer interface

#### func (Collection) Supply

```go
func (collection Collection) Supply() int
```
Supply gets the total supply of NFTs of a collection

#### func (Collection) UpdateNFT

```go
func (collection Collection) UpdateNFT(nft exported.NFT) (Collection, sdk.Error)
```
UpdateNFT updates an NFT from a collection

#### type CollectionJSON

```go
type CollectionJSON map[string]Collection
```

CollectionJSON is the exported Collection format for clients

#### type Collections

```go
type Collections []Collection
```

Collections define an array of Collection

#### func  NewCollections

```go
func NewCollections(collections ...Collection) Collections
```
NewCollections creates a new set of NFTs

#### func (Collections) Append

```go
func (collections Collections) Append(collectionsB ...Collection) Collections
```
Append appends two sets of Collections

#### func (Collections) ElAtIndex

```go
func (collections Collections) ElAtIndex(index int) string
```

#### func (Collections) Empty

```go
func (collections Collections) Empty() bool
```
Empty returns true if there are no collections and false otherwise.

#### func (Collections) Find

```go
func (collections Collections) Find(denom string) (Collection, bool)
```
Find returns the searched collection from the set

#### func (Collections) Len

```go
func (collections Collections) Len() int
```

#### func (Collections) Less

```go
func (collections Collections) Less(i, j int) bool
```

#### func (Collections) MarshalJSON

```go
func (collections Collections) MarshalJSON() ([]byte, error)
```
MarshalJSON for Collections

#### func (Collections) Remove

```go
func (collections Collections) Remove(denom string) (Collections, bool)
```
Remove removes a collection from the set of collections

#### func (Collections) Sort

```go
func (collections Collections) Sort() Collections
```
Sort is a helper function to sort the set of coins inplace

#### func (Collections) String

```go
func (collections Collections) String() string
```
String follows stringer interface

#### func (Collections) Swap

```go
func (collections Collections) Swap(i, j int)
```

#### func (*Collections) UnmarshalJSON

```go
func (collections *Collections) UnmarshalJSON(b []byte) error
```
UnmarshalJSON for Collections

#### type Findable

```go
type Findable interface {
	ElAtIndex(index int) string
	Len() int
}
```

Findable is an interface for iterable types that allows the FindUtil function to
work

#### type GenesisState

```go
type GenesisState struct {
	Owners      []Owner     `json:"owners"`
	Collections Collections `json:"collections"`
}
```

GenesisState is the state that must be provided at genesis.

#### func  DefaultGenesisState

```go
func DefaultGenesisState() GenesisState
```
DefaultGenesisState returns a default genesis state

#### func  NewGenesisState

```go
func NewGenesisState(owners []Owner, collections Collections) GenesisState
```
NewGenesisState creates a new genesis state.

#### type IDCollection

```go
type IDCollection struct {
	Denom string            `json:"denom" yaml:"denom"`
	IDs   SortedStringArray `json:"ids" yaml:"ids"`
}
```

IDCollection defines a set of nft ids that belong to a specific collection

#### func  NewIDCollection

```go
func NewIDCollection(denom string, ids []string) IDCollection
```
NewIDCollection creates a new IDCollection instance

#### func (IDCollection) AddID

```go
func (idCollection IDCollection) AddID(id string) IDCollection
```
AddID adds an ID to the idCollection

#### func (IDCollection) DeleteID

```go
func (idCollection IDCollection) DeleteID(id string) (IDCollection, sdk.Error)
```
DeleteID deletes an ID from an ID Collection

#### func (IDCollection) Exists

```go
func (idCollection IDCollection) Exists(id string) (exists bool)
```
Exists determines whether an ID is in the IDCollection

#### func (IDCollection) String

```go
func (idCollection IDCollection) String() string
```
String follows stringer interface

#### func (IDCollection) Supply

```go
func (idCollection IDCollection) Supply() int
```
Supply gets the total supply of NFTIDs of a balance

#### type IDCollections

```go
type IDCollections []IDCollection
```

IDCollections is an array of ID Collections whose sole purpose is for find

#### func (IDCollections) Append

```go
func (idCollections IDCollections) Append(idCollections2 ...IDCollection) IDCollections
```
Append appends IDCollections to IDCollections

#### func (IDCollections) ElAtIndex

```go
func (idCollections IDCollections) ElAtIndex(index int) string
```

#### func (IDCollections) Len

```go
func (idCollections IDCollections) Len() int
```

#### func (IDCollections) Less

```go
func (idCollections IDCollections) Less(i, j int) bool
```

#### func (IDCollections) Sort

```go
func (idCollections IDCollections) Sort() IDCollections
```
Sort is a helper function to sort the set of strings in place

#### func (IDCollections) String

```go
func (idCollections IDCollections) String() string
```
String follows stringer interface

#### func (IDCollections) Swap

```go
func (idCollections IDCollections) Swap(i, j int)
```

#### type MsgBurnNFT

```go
type MsgBurnNFT struct {
	Sender sdk.AccAddress `json:"sender" yaml:"sender"`
	ID     string         `json:"id" yaml:"id"`
	Denom  string         `json:"denom" yaml:"denom"`
}
```

MsgBurnNFT defines a BurnNFT message

#### func  NewMsgBurnNFT

```go
func NewMsgBurnNFT(sender sdk.AccAddress, id string, denom string) MsgBurnNFT
```
NewMsgBurnNFT is a constructor function for MsgBurnNFT

#### func (MsgBurnNFT) GetSignBytes

```go
func (msg MsgBurnNFT) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgBurnNFT) GetSigners

```go
func (msg MsgBurnNFT) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgBurnNFT) Route

```go
func (msg MsgBurnNFT) Route() string
```
Route Implements Msg

#### func (MsgBurnNFT) Type

```go
func (msg MsgBurnNFT) Type() string
```
Type Implements Msg

#### func (MsgBurnNFT) ValidateBasic

```go
func (msg MsgBurnNFT) ValidateBasic() sdk.Error
```
ValidateBasic Implements Msg.

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

#### func  NewMsgEditNFTMetadata

```go
func NewMsgEditNFTMetadata(sender sdk.AccAddress, id,
	denom, tokenURI string,
) MsgEditNFTMetadata
```
NewMsgEditNFTMetadata is a constructor function for MsgSetName

#### func (MsgEditNFTMetadata) GetSignBytes

```go
func (msg MsgEditNFTMetadata) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgEditNFTMetadata) GetSigners

```go
func (msg MsgEditNFTMetadata) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgEditNFTMetadata) Route

```go
func (msg MsgEditNFTMetadata) Route() string
```
Route Implements Msg

#### func (MsgEditNFTMetadata) Type

```go
func (msg MsgEditNFTMetadata) Type() string
```
Type Implements Msg

#### func (MsgEditNFTMetadata) ValidateBasic

```go
func (msg MsgEditNFTMetadata) ValidateBasic() sdk.Error
```
ValidateBasic Implements Msg.

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

#### func  NewMsgMintNFT

```go
func NewMsgMintNFT(sender, recipient sdk.AccAddress, id, denom, tokenURI string) MsgMintNFT
```
NewMsgMintNFT is a constructor function for MsgMintNFT

#### func (MsgMintNFT) GetSignBytes

```go
func (msg MsgMintNFT) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgMintNFT) GetSigners

```go
func (msg MsgMintNFT) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgMintNFT) Route

```go
func (msg MsgMintNFT) Route() string
```
Route Implements Msg

#### func (MsgMintNFT) Type

```go
func (msg MsgMintNFT) Type() string
```
Type Implements Msg

#### func (MsgMintNFT) ValidateBasic

```go
func (msg MsgMintNFT) ValidateBasic() sdk.Error
```
ValidateBasic Implements Msg.

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

#### func  NewMsgTransferNFT

```go
func NewMsgTransferNFT(sender, recipient sdk.AccAddress, denom, id string) MsgTransferNFT
```
NewMsgTransferNFT is a constructor function for MsgSetName

#### func (MsgTransferNFT) GetSignBytes

```go
func (msg MsgTransferNFT) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgTransferNFT) GetSigners

```go
func (msg MsgTransferNFT) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgTransferNFT) Route

```go
func (msg MsgTransferNFT) Route() string
```
Route Implements Msg

#### func (MsgTransferNFT) Type

```go
func (msg MsgTransferNFT) Type() string
```
Type Implements Msg

#### func (MsgTransferNFT) ValidateBasic

```go
func (msg MsgTransferNFT) ValidateBasic() sdk.Error
```
ValidateBasic Implements Msg.

#### type NFTJSON

```go
type NFTJSON map[string]BaseNFT
```

NFTJSON is the exported NFT format for clients

#### type NFTs

```go
type NFTs []exported.NFT
```

NFTs define a list of NFT

#### func  NewNFTs

```go
func NewNFTs(nfts ...exported.NFT) NFTs
```
NewNFTs creates a new set of NFTs

#### func (NFTs) Append

```go
func (nfts NFTs) Append(nftsB ...exported.NFT) NFTs
```
Append appends two sets of NFTs

#### func (NFTs) ElAtIndex

```go
func (nfts NFTs) ElAtIndex(index int) string
```
Findable and Sort interfaces

#### func (NFTs) Empty

```go
func (nfts NFTs) Empty() bool
```
Empty returns true if there are no NFTs and false otherwise.

#### func (NFTs) Find

```go
func (nfts NFTs) Find(id string) (nft exported.NFT, found bool)
```
Find returns the searched collection from the set

#### func (NFTs) Len

```go
func (nfts NFTs) Len() int
```

#### func (NFTs) Less

```go
func (nfts NFTs) Less(i, j int) bool
```

#### func (NFTs) MarshalJSON

```go
func (nfts NFTs) MarshalJSON() ([]byte, error)
```
MarshalJSON for NFTs

#### func (NFTs) Remove

```go
func (nfts NFTs) Remove(id string) (NFTs, bool)
```
Remove removes an NFT from the set of NFTs

#### func (NFTs) Sort

```go
func (nfts NFTs) Sort() NFTs
```
Sort is a helper function to sort the set of coins in place

#### func (NFTs) String

```go
func (nfts NFTs) String() string
```
String follows stringer interface

#### func (NFTs) Swap

```go
func (nfts NFTs) Swap(i, j int)
```

#### func (*NFTs) UnmarshalJSON

```go
func (nfts *NFTs) UnmarshalJSON(b []byte) error
```
UnmarshalJSON for NFTs

#### func (NFTs) Update

```go
func (nfts NFTs) Update(id string, nft exported.NFT) (NFTs, bool)
```
Update removes and replaces an NFT from the set

#### type Owner

```go
type Owner struct {
	Address       sdk.AccAddress `json:"address" yaml:"address"`
	IDCollections IDCollections  `json:"idCollections" yaml:"idCollections"`
}
```

Owner of non fungible tokens

#### func  NewOwner

```go
func NewOwner(owner sdk.AccAddress, idCollections ...IDCollection) Owner
```
NewOwner creates a new Owner

#### func (Owner) DeleteID

```go
func (owner Owner) DeleteID(denom string, id string) (Owner, sdk.Error)
```
DeleteID deletes an ID from an owners ID Collection

#### func (Owner) GetIDCollection

```go
func (owner Owner) GetIDCollection(denom string) (IDCollection, bool)
```
GetIDCollection gets the IDCollection from the owner

#### func (Owner) String

```go
func (owner Owner) String() string
```
String follows stringer interface

#### func (Owner) Supply

```go
func (owner Owner) Supply() int
```
Supply gets the total supply of an Owner

#### func (Owner) UpdateIDCollection

```go
func (owner Owner) UpdateIDCollection(idCollection IDCollection) (Owner, sdk.Error)
```
UpdateIDCollection updates the ID Collection of an owner

#### type QueryBalanceParams

```go
type QueryBalanceParams struct {
	Owner sdk.AccAddress
	Denom string // optional
}
```

QueryBalanceParams params for query 'custom/nfts/balance'

#### func  NewQueryBalanceParams

```go
func NewQueryBalanceParams(owner sdk.AccAddress, denom ...string) QueryBalanceParams
```
NewQueryBalanceParams creates a new instance of QuerySupplyParams

#### type QueryCollectionParams

```go
type QueryCollectionParams struct {
	Denom string
}
```

QueryCollectionParams defines the params for queries: - 'custom/nft/supply' -
'custom/nft/collection'

#### func  NewQueryCollectionParams

```go
func NewQueryCollectionParams(denom string) QueryCollectionParams
```
NewQueryCollectionParams creates a new instance of QuerySupplyParams

#### func (QueryCollectionParams) Bytes

```go
func (q QueryCollectionParams) Bytes() []byte
```
Bytes exports the Denom as bytes

#### type QueryNFTParams

```go
type QueryNFTParams struct {
	Denom   string
	TokenID string
}
```

QueryNFTParams params for query 'custom/nfts/nft'

#### func  NewQueryNFTParams

```go
func NewQueryNFTParams(denom, id string) QueryNFTParams
```
NewQueryNFTParams creates a new instance of QueryNFTParams

#### type SortedStringArray

```go
type SortedStringArray []string
```

SortedStringArray is an array of strings whose sole purpose is to help with find

#### func (SortedStringArray) ElAtIndex

```go
func (sa SortedStringArray) ElAtIndex(index int) string
```

#### func (SortedStringArray) Len

```go
func (sa SortedStringArray) Len() int
```

#### func (SortedStringArray) Less

```go
func (sa SortedStringArray) Less(i, j int) bool
```

#### func (SortedStringArray) Sort

```go
func (sa SortedStringArray) Sort() SortedStringArray
```
Sort is a helper function to sort the set of strings in place

#### func (SortedStringArray) String

```go
func (sa SortedStringArray) String() string
```
String is the string representation

#### func (SortedStringArray) Swap

```go
func (sa SortedStringArray) Swap(i, j int)
```
