# types
--
    import "github.com/xar-network/xar-network/x/record/internal/types"


## Usage

```go
const (
	// ModuleKey is the name of the module
	ModuleName = "record"
	// StoreKey is the store key string for record
	StoreKey = ModuleName
	// RouterKey is the message route for record
	RouterKey = ModuleName
	// QuerierRoute is the querier route for record
	QuerierRoute = ModuleName
	// Parameter store default namestore
	DefaultParamspace = ModuleName
)
```

```go
const (
	IDPreStr = "rec"
	Custom   = "custom"
)
```

```go
const (
	QueryParams  = "params"
	QueryRecords = "list"
	QueryRecord  = "query"
	QuerySearch  = "search"
)
```

```go
const (
	CodeInvalidGenesis   sdk.CodeType = 102
	HashLength                        = 64
	NameMinLength                     = 3
	NameMaxLength                     = 32
	AuthorMaxLength                   = 64
	RecordTypeMaxLength               = 32
	RecordNoMaxLength                 = 32
	DescriptionMaxLength              = 1024
)
```

```go
const (
	CodeRecordExist          sdk.CodeType = 1
	CodeRecordHashNotValid   sdk.CodeType = 2
	CodeRecordIDNotValid     sdk.CodeType = 3
	CodeRecordNumberNotValid sdk.CodeType = 4
	CodeRecordNameNotValid   sdk.CodeType = 5
	CodeRecordAuthorNotValid sdk.CodeType = 6
	CodeRecordTypeNotValid   sdk.CodeType = 7
	CodeDescriptionNotValid  sdk.CodeType = 8
	CodeUnknownRecord        sdk.CodeType = 9
	CodeUnknownAuthor        sdk.CodeType = 10
)
```

```go
const (
	DefaultCodespace sdk.CodespaceType = ModuleName
)
```

```go
const (
	TypeMsgRecord = "record"
)
```

```go
var (
	RecordMaxId uint64 = 999999999999
	RecordMinId uint64 = 100000000000
)
```

```go
var (
	TxCategory = "record"

	Action     = sdk.AttributeKeyAction
	Category   = "category"
	Sender     = sdk.AttributeKeySender
	ID         = "id"
	Name       = "name"
	Hash       = "hash"
	Author     = "author"
	RecordType = "record-type"
	RecordNo   = "record-number"
)
```
Record tags

```go
var ModuleCdc = codec.New()
```

#### func  CheckRecordHash

```go
func CheckRecordHash(hash string) sdk.Error
```

#### func  CheckRecordId

```go
func CheckRecordId(issueID string) sdk.Error
```

#### func  ErrDescriptionNotValid

```go
func ErrDescriptionNotValid() sdk.Error
```

#### func  ErrRecordAuthorNotValid

```go
func ErrRecordAuthorNotValid() sdk.Error
```

#### func  ErrRecordExist

```go
func ErrRecordExist(record string) sdk.Error
```
Error constructors

#### func  ErrRecordHashNotValid

```go
func ErrRecordHashNotValid() sdk.Error
```

#### func  ErrRecordIDNotValid

```go
func ErrRecordIDNotValid(recordID string) sdk.Error
```

#### func  ErrRecordNameNotValid

```go
func ErrRecordNameNotValid() sdk.Error
```

#### func  ErrRecordNumberNotValid

```go
func ErrRecordNumberNotValid() sdk.Error
```

#### func  ErrRecordTypeNotValid

```go
func ErrRecordTypeNotValid() sdk.Error
```

#### func  ErrUnknownAuthor

```go
func ErrUnknownAuthor(author string) sdk.Error
```

#### func  ErrUnknownRecord

```go
func ErrUnknownRecord(record string) sdk.Error
```

#### func  Errorf

```go
func Errorf(err sdk.Error) error
```
convert sdk.Error to error

#### func  GetRandomString

```go
func GetRandomString(l int) string
```

#### func  GetRecordTags

```go
func GetRecordTags(info *RecordInfo) sdk.Events
```

#### func  IsRecordId

```go
func IsRecordId(id string) bool
```

#### func  RegisterCodec

```go
func RegisterCodec(cdc *codec.Codec)
```
Register concrete types on codec codec

#### type MsgFlag

```go
type MsgFlag interface {
	sdk.Msg

	GetRecordId() string
	SetRecordId(string)

	GetSender() sdk.AccAddress
	SetSender(sdk.AccAddress)
}
```


#### type MsgRecord

```go
type MsgRecord struct {
	Sender        sdk.AccAddress `json:"sender" yaml:"sender"`
	*RecordParams `json:"params" yaml:"params"`
}
```

MsgRecord to allow a registered recordr to record new coins.

#### func  NewMsgRecord

```go
func NewMsgRecord(sender sdk.AccAddress, params *RecordParams) MsgRecord
```
New MsgRecord Instance

#### func (MsgRecord) GetSignBytes

```go
func (msg MsgRecord) GetSignBytes() []byte
```
GetSignBytes Implements Msg.

#### func (MsgRecord) GetSigners

```go
func (msg MsgRecord) GetSigners() []sdk.AccAddress
```
GetSigners Implements Msg.

#### func (MsgRecord) Route

```go
func (msg MsgRecord) Route() string
```
Route Implements Msg.

#### func (MsgRecord) String

```go
func (msg MsgRecord) String() string
```

#### func (MsgRecord) Type

```go
func (msg MsgRecord) Type() string
```
Type Implements Msg.

#### func (MsgRecord) ValidateBasic

```go
func (msg MsgRecord) ValidateBasic() sdk.Error
```
Implements Msg. Ensures addresses are valid and Coin is positive

#### type Record

```go
type Record interface {
	GetID() string
	SetID(string)

	GetHash() string
	SetHash(string)

	GetRecordNo() string
	SetRecordNo(string)

	GetSender() sdk.AccAddress
	SetSender(sdk.AccAddress)

	GetRecordTime() int64
	SetRecordTime(int64)

	GetName() string
	SetName(string)

	GetAuthor() string
	SetAuthor(string)

	GetRecordType() string
	SetRecordType(string)

	GetDescription() string
	SetDescription(string)

	String() string
}
```

Record interface

#### type RecordInfo

```go
type RecordInfo struct {
	ID          string         `json:"id"`
	Hash        string         `json:"hash"`
	RecordNo    string         `json:"record_number"`
	Sender      sdk.AccAddress `json:"sender"`
	RecordTime  int64          `json:"record_time"`
	Name        string         `json:"name"`
	Author      string         `json:"author"`
	RecordType  string         `json:"record_type"`
	Description string         `json:"description"`
}
```

Record Info

#### func (RecordInfo) GetAuthor

```go
func (ci RecordInfo) GetAuthor() string
```

#### func (RecordInfo) GetDescription

```go
func (ci RecordInfo) GetDescription() string
```

#### func (RecordInfo) GetHash

```go
func (ci RecordInfo) GetHash() string
```

#### func (RecordInfo) GetID

```go
func (ci RecordInfo) GetID() string
```
nolint

#### func (RecordInfo) GetName

```go
func (ci RecordInfo) GetName() string
```

#### func (RecordInfo) GetRecordNo

```go
func (ci RecordInfo) GetRecordNo() string
```

#### func (RecordInfo) GetRecordTime

```go
func (ci RecordInfo) GetRecordTime() int64
```

#### func (RecordInfo) GetRecordType

```go
func (ci RecordInfo) GetRecordType() string
```

#### func (RecordInfo) GetSender

```go
func (ci RecordInfo) GetSender() sdk.AccAddress
```

#### func (*RecordInfo) SetAuthor

```go
func (ci *RecordInfo) SetAuthor(author string)
```

#### func (*RecordInfo) SetDescription

```go
func (ci *RecordInfo) SetDescription(description string)
```

#### func (*RecordInfo) SetHash

```go
func (ci *RecordInfo) SetHash(hash string)
```

#### func (*RecordInfo) SetID

```go
func (ci *RecordInfo) SetID(id string)
```

#### func (*RecordInfo) SetName

```go
func (ci *RecordInfo) SetName(name string)
```

#### func (*RecordInfo) SetRecordNo

```go
func (ci *RecordInfo) SetRecordNo(number string)
```

#### func (*RecordInfo) SetRecordTime

```go
func (ci *RecordInfo) SetRecordTime(time int64)
```

#### func (*RecordInfo) SetRecordType

```go
func (ci *RecordInfo) SetRecordType(recordType string)
```

#### func (*RecordInfo) SetSender

```go
func (ci *RecordInfo) SetSender(operator sdk.AccAddress)
```

#### func (RecordInfo) String

```go
func (ci RecordInfo) String() string
```
nolint

#### type RecordParams

```go
type RecordParams struct {
	Name        string `json:"name" yaml:"name"`
	Author      string `json:"author" yaml:"author"`
	Hash        string `json:"hash" yaml:"hash"`
	RecordNo    string `json:"record_number" yaml:"record_number"`
	RecordType  string `json:"record_type" yaml:"record_type"`
	Description string `json:"description" yaml:"description"`
}
```

Param for record

#### type RecordQueryParams

```go
type RecordQueryParams struct {
	StartRecordId string         `json:"start_record_id"`
	Sender        sdk.AccAddress `json:"sender"`
	Limit         int            `json:"limit"`
}
```

Param for query record

#### type Records

```go
type Records []RecordInfo
```

Records is an array of Record

#### func (Records) String

```go
func (records Records) String() string
```
nolint
