# order
--
    import "github.com/xar-network/xar-network/x/order/types"


## Usage

```go
const (
	// ModuleName The name that will be used throughout the module
	ModuleName = "order"

	// StoreKey Top level store key where all module items will be stored
	StoreKey = ModuleName

	// RouterKey Top level router key
	RouterKey = ModuleName

	// DefaultParamspace default name for parameter store
	DefaultParamspace = ModuleName
)
```

```go
const MaxTimeInForce = 600
```

```go
var ModuleCdc = codec.New()
```

#### func  RegisterCodec

```go
func RegisterCodec(cdc *codec.Codec)
```

#### type ListQueryResult

```go
type ListQueryResult struct {
	Orders []Order `json:"orders"`
}
```


#### func (ListQueryResult) String

```go
func (l ListQueryResult) String() string
```

#### type MsgCancel

```go
type MsgCancel struct {
	Owner   sdk.AccAddress `json:"owner" yaml:"owner"`
	OrderID store.EntityID `json:"order_id" yaml:"order_id"`
}
```


#### func  NewMsgCancel

```go
func NewMsgCancel(owner sdk.AccAddress, orderID store.EntityID) MsgCancel
```

#### func (MsgCancel) GetSignBytes

```go
func (msg MsgCancel) GetSignBytes() []byte
```

#### func (MsgCancel) GetSigners

```go
func (msg MsgCancel) GetSigners() []sdk.AccAddress
```

#### func (MsgCancel) Route

```go
func (msg MsgCancel) Route() string
```

#### func (MsgCancel) Type

```go
func (msg MsgCancel) Type() string
```

#### func (MsgCancel) ValidateBasic

```go
func (msg MsgCancel) ValidateBasic() sdk.Error
```

#### type MsgPost

```go
type MsgPost struct {
	Owner       sdk.AccAddress     `json:"owner" yaml:"owner"`
	MarketID    store.EntityID     `json:"market_id" yaml:"market_id"`
	Direction   matcheng.Direction `json:"direction" yaml:"direction"`
	Price       sdk.Uint           `json:"price" yaml:"price"`
	Quantity    sdk.Uint           `json:"quantity" yaml:"quantity"`
	TimeInForce uint16             `json:"time_in_force" yaml:"time_in_force"`
}
```


#### func  NewMsgPost

```go
func NewMsgPost(owner sdk.AccAddress, marketID store.EntityID, direction matcheng.Direction, price sdk.Uint, quantity sdk.Uint, tif uint16) MsgPost
```

#### func (MsgPost) GetSignBytes

```go
func (msg MsgPost) GetSignBytes() []byte
```

#### func (MsgPost) GetSigners

```go
func (msg MsgPost) GetSigners() []sdk.AccAddress
```

#### func (MsgPost) Route

```go
func (msg MsgPost) Route() string
```

#### func (MsgPost) Type

```go
func (msg MsgPost) Type() string
```

#### func (MsgPost) ValidateBasic

```go
func (msg MsgPost) ValidateBasic() sdk.Error
```

#### type Order

```go
type Order struct {
	ID                store.EntityID     `json:"id"`
	Owner             sdk.AccAddress     `json:"owner"`
	MarketID          store.EntityID     `json:"market"`
	Direction         matcheng.Direction `json:"direction"`
	Price             sdk.Uint           `json:"price"`
	Quantity          sdk.Uint           `json:"quantity"`
	TimeInForceBlocks uint16             `json:"time_in_force_blocks"`
	CreatedBlock      int64              `json:"created_block"`
}
```


#### func  New

```go
func New(owner sdk.AccAddress, marketID store.EntityID, direction matcheng.Direction, price sdk.Uint, quantity sdk.Uint, tif uint16, created int64) Order
```
