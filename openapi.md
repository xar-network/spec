# Xar Network
A REST interface for state queries, transaction generation and broadcasting.

## Version: 3.0

### /auth/login

#### POST
##### Summary:

Logs a user in.

##### Description:

Logs a user in.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| body | body |  | No | [body](#body) |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 204 | User successfully logged in. The session ID is returned in a cookie. |  |
| 403 | Authentication failed. |  |

### /auth/logout

#### POST
##### Summary:

Logs a user out.

##### Description:

Logs a user out.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |

##### Responses

| Code | Description |
| ---- | ----------- |
| 204 | User successfully logged out. |

### /auth/change_password

#### POST
##### Summary:

Changes a user's password.

##### Description:

All sessions using the previous password will be logged out.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| body | body |  | No | [body_1](#body_1) |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 204 | Password successfully changed. |  |
| 403 | Invalid password. |  |

### /exchange/orders

#### PUT
##### Summary:

Modifies an existing order. Funds will immediately debited if the quantity increases, or credited if the quantity decreases.

##### Description:

Modifies an existing order. Funds will immediately debited if the quantity increases, or credited if the quantity decreases.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| body | body |  | Yes | [Order](#order) |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Order successfully modified. | [OrderCreationResponse](#ordercreationresponse) |

#### POST
##### Summary:

Posts an order. Funds will be immediately debited.

##### Description:

Posts an order. Funds will be immediately debited.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| body | body |  | Yes | [OrderCreationRequest](#ordercreationrequest) |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 204 | Order successfully posted. | [OrderCreationResponse](#ordercreationresponse) |

### /exchange/orders/{order_id}

#### GET
##### Summary:

Gets an order by its ID.

##### Description:

Gets an order by its ID.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| order_id | path | Numeric ID of the order. | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returns the looked-up order. | [OrderWithFills](#orderwithfills) |
| 404 | Order not found. |  |

#### DELETE
##### Summary:

Cancels an order by its ID.

##### Description:

Cancels an order by its ID.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| order_id | path | Numeric ID of the order. | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Order successfully cancelled. | [BlockInclusionResponse](#blockinclusionresponse) |
| 403 | Order is not owned by current user. |  |
| 404 | Order not found. |  |
| 422 | Order is already cancelled. |  |

### /exchange/orders/cancel

#### POST
##### Summary:

Cancels a group of orders.

##### Description:

Cancels a group of orders.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| body | body |  | Yes | [body_2](#body_2) |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Bulk cancel completed. Some response may have failed; see the response body itself to deal with individual errors. | [ object ] |

### /user/balance

#### GET
##### Summary:

Returns the user's balance across all supported chains.

##### Description:

Returns the user's balance across all supported chains.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The user's balances. | [Balance](#balance) |

### /user/orders

#### GET
##### Summary:

Gets all orders created by this user.

##### Description:

Gets all orders created by this user.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| start | query | The ID to begin counting at. | No | integer |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The user's orders. | [inline_response_200](#inline_response_200) |

### /user/fills

#### GET
##### Summary:

Gets all fills relevant to this user.

##### Description:

Gets all fills relevant to this user.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| start_block | query | The block to start counting from. | No | integer |
| end_block | query | The block to end counting at. | No | integer |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The user's fills. | [inline_response_200_1](#inline_response_200_1) |

### /user/send

#### POST
##### Summary:

Transfers Funds

##### Description:

Transfers Funds

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| body | body |  | Yes | [body_3](#body_3) |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Status of the transfer. | [BlockInclusionResponse](#blockinclusionresponse) |

### /user/withdrawals

#### GET
##### Summary:

Gets the user's list of withdrawals.

##### Description:

Gets the user's list of withdrawals.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | List of withdrawals. | [inline_response_200_2](#inline_response_200_2) |

#### POST
##### Summary:

Initiates a withdrawal of a cleared asset.

##### Description:

Initiates a withdrawal of a cleared asset.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| body | body |  | Yes | [body_4](#body_4) |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Withdrawal successfully initiated. | [Withdrawal](#withdrawal) |

### /user/deposits

#### POST
##### Summary:

Registers a relay chain deposit on the DEX demo.

##### Description:

Registers a relay chain deposit on the DEX demo.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| body | body |  | Yes | [body_5](#body_5) |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Deposit successfully initiated. | [BlockInclusionResponse](#blockinclusionresponse) |

### /markets/{market_id}/candles

#### GET
##### Summary:

Gets candlestick prices for the provided market.

##### Description:

Gets candlestick prices for the provided market.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| market_id | path | The ID of the market to fetch candles for. | Yes | string |
| start | query | ISO8601 date of when to start the candle query. | No | string |
| end | query | ISO8601 date of when to end the candle query. | No | string |
| granularity | query | Granularity of candle data to return. | No | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Candle data. | [CandlestickResponse](#candlestickresponse) |

### /markets/{market_id}/spread/{block_number}

#### GET
##### Summary:

Gets the batch auction state for the provided market ID and the block number.

##### Description:

Gets the batch auction state for the provided market ID and the block number.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| market_id | path |  | Yes | string |
| block_number | path |  | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The batch state. | [Spread](#spread) |

### /markets/{market_id}/book

#### GET
##### Summary:

Gets all open order at latest block by market

##### Description:

Gets all open order at latest block by market

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| market_id | path |  | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The batch state. | [Spread](#spread) |

### /markets/{market_id}/batches/{block_number}

#### GET
##### Summary:

Gets all executed batches at a block (or latest)

##### Description:

Gets all executed batches at a block (or latest)

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| market_id | path |  | Yes | string |
| block_number | path |  | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The batch state. | [BatchesResponse](#batchesresponse) |

### /markets/{market_id}/daily

#### GET
##### Summary:

Daily Price Stats

##### Description:

Daily Price Stats

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| market_id | path |  | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The stats. | [inline_response_200_3](#inline_response_200_3) |

### /markets

#### GET
##### Summary:

Lists all markets.

##### Description:

Lists all markets.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | List of markets. | [Market](#market) |

### /node_info

#### GET
##### Summary:

The properties of the connected node

##### Description:

Information about the connected node

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Node status | [node_info](#node_info) |
| 500 | Failed to query node status |  |

### /syncing

#### GET
##### Summary:

Syncing state of node

##### Description:

Get if the node is currently syning with other nodes

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | "true" or "false" | [sync](#sync) |
| 500 | Server internal error |  |

### /blocks/latest

#### GET
##### Summary:

Get the latest block

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The latest block | [block_query](#block_query) |
| 500 | Server internal error |  |

### /blocks/{height}

#### GET
##### Summary:

Get a block at a certain height

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| height | path | Block height | Yes | number |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The block at a specific height | [block_query](#block_query) |
| 400 | Invalid height |  |
| 404 | Request block height doesn't |  |
| 500 | Server internal error |  |

### /validatorsets/latest

#### GET
##### Summary:

Get the latest validator set

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The validator set at the latest block height | [validator_set](#validator_set) |
| 500 | Server internal error |  |

### /validatorsets/{height}

#### GET
##### Summary:

Get a validator set a certain height

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| height | path | Block height | Yes | number |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The validator set at a specific block height | [validator_set](#validator_set) |
| 400 | Invalid height |  |
| 404 | Block at height not available |  |
| 500 | Server internal error |  |

### /txs/{hash}

#### GET
##### Summary:

Get a Tx by hash

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| hash | path | Tx hash | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Tx with the provided hash | [tx](#tx) |
| 500 | Internal Server Error |  |

### /txs

#### GET
##### Summary:

Search transactions

##### Description:

Search transactions by tag(s).

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| tag | query | transaction tags such as 'action=submit-proposal' and 'proposer=xar1hkc7l5jmsmrmsmsre7qsatrx5wjgan942c77ac' which results in the following endpoint: 'GET /txs?action=submit-proposal&proposer=xar1hkc7l5jmsmrmsmsre7qsatrx5wjgan942c77ac' | Yes | string |
| page | query | Page number | No | integer |
| limit | query | Maximum number of items per page | No | integer |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | All txs matching the provided tags | [ [tx](#tx) ] |
| 400 | Invalid search tags |  |
| 500 | Internal Server Error |  |

#### POST
##### Summary:

Broadcast a signed tx

##### Description:

Broadcast a signed tx to a full node

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| txBroadcast | body | The tx must be a signed StdTx. The supported broadcast modes include `"block"`(return after tx commit), `"sync"`(return afer CheckTx) and `"async"`(return right away). | Yes | object |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Tx broadcasting result | [BroadcastTxCommitResult](#broadcasttxcommitresult) |
| 500 | Internal Server Error |  |

### /txs/encode

#### POST
##### Summary:

Encode a transaction to the Amino wire format

##### Description:

Encode a transaction (signed or not) from JSON to base64-encoded Amino serialized bytes

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| tx | body | The tx to encode | Yes | object |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The tx was successfully decoded and re-encoded | object |
| 400 | The tx was malformated |  |
| 500 | Server internal error |  |

### /bank/balances/{address}

#### GET
##### Summary:

Get the account balances

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| address | path | Account address in bech32 format | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Account balances | [ [balances](#balances) ] |
| 204 | There is no data for the requested account |  |
| 500 | Server internal error |  |

### /bank/accounts/{address}/transfers

#### POST
##### Summary:

Send coins from one account to another

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| address | path | Account address in bech32 format | Yes | string |
| account | body | The sender and tx information | Yes | object |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 202 | Tx was succesfully generated | [StdTx](#stdtx) |
| 400 | Invalid request |  |
| 500 | Server internal error |  |

### /auth/accounts/{address}

#### GET
##### Summary:

Get the account information on blockchain

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| address | path | Account address | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Account information on the blockchain | [accounts](#accounts) |
| 204 | No content about this account address |  |
| 500 | Server internel error |  |

### /staking/delegators/{delegatorAddr}/delegations

#### GET
##### Summary:

Get all delegations from a delegator

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| delegatorAddr | path | Bech32 AccAddress of Delegator | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [ [Delegation](#delegation) ] |
| 400 | Invalid delegator address |  |
| 500 | Internal Server Error |  |

#### POST
##### Summary:

Submit delegation

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| delegatorAddr | path | Bech32 AccAddress of Delegator | Yes | string |
| delegation | body | The password of the account to remove from the KMS | No | object |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [BroadcastTxCommitResult](#broadcasttxcommitresult) |
| 400 | Invalid delegator address or delegation request body |  |
| 401 | Key password is wrong |  |
| 500 | Internal Server Error |  |

### /staking/delegators/{delegatorAddr}/delegations/{validatorAddr}

#### GET
##### Summary:

Query the current delegation between a delegator and a validator

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| delegatorAddr | path | Bech32 AccAddress of Delegator | Yes | string |
| validatorAddr | path | Bech32 OperatorAddress of validator | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Delegation](#delegation) |
| 400 | Invalid delegator address or validator address |  |
| 500 | Internal Server Error |  |

### /staking/delegators/{delegatorAddr}/unbonding_delegations

#### GET
##### Summary:

Get all unbonding delegations from a delegator

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| delegatorAddr | path | Bech32 AccAddress of Delegator | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [ [UnbondingDelegation](#unbondingdelegation) ] |
| 400 | Invalid delegator address |  |
| 500 | Internal Server Error |  |

#### POST
##### Summary:

Submit an unbonding delegation

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| delegatorAddr | path | Bech32 AccAddress of Delegator | Yes | string |
| delegation | body | The password of the account to remove from the KMS | No | object |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [BroadcastTxCommitResult](#broadcasttxcommitresult) |
| 400 | Invalid delegator address or unbonding delegation request body |  |
| 401 | Key password is wrong |  |
| 500 | Internal Server Error |  |

### /staking/delegators/{delegatorAddr}/unbonding_delegations/{validatorAddr}

#### GET
##### Summary:

Query all unbonding delegations between a delegator and a validator

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| delegatorAddr | path | Bech32 AccAddress of Delegator | Yes | string |
| validatorAddr | path | Bech32 OperatorAddress of validator | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [ [UnbondingDelegation](#unbondingdelegation) ] |
| 400 | Invalid delegator address or validator address |  |
| 500 | Internal Server Error |  |

### /staking/redelegations

#### GET
##### Summary:

Get all redelegations (filter by query params)

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| delegator | query | Bech32 AccAddress of Delegator | No | string |
| validator_from | query | Bech32 ValAddress of SrcValidator | No | string |
| validator_to | query | Bech32 ValAddress of DstValidator | No | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [ [Redelegation](#redelegation) ] |
| 500 | Internal Server Error |  |

### /staking/delegators/{delegatorAddr}/redelegations

#### POST
##### Summary:

Submit a redelegation

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| delegatorAddr | path | Bech32 AccAddress of Delegator | Yes | string |
| delegation | body | The sender and tx information | No | object |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Tx was succesfully generated | [StdTx](#stdtx) |
| 400 | Invalid delegator address or redelegation request body |  |
| 500 | Internal Server Error |  |

### /staking/delegators/{delegatorAddr}/validators

#### GET
##### Summary:

Query all validators that a delegator is bonded to

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| delegatorAddr | path | Bech32 AccAddress of Delegator | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [ [Validator](#validator) ] |
| 400 | Invalid delegator address |  |
| 500 | Internal Server Error |  |

### /staking/delegators/{delegatorAddr}/validators/{validatorAddr}

#### GET
##### Summary:

Query a validator that a delegator is bonded to

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| delegatorAddr | path | Bech32 AccAddress of Delegator | Yes | string |
| validatorAddr | path | Bech32 ValAddress of Delegator | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Validator](#validator) |
| 400 | Invalid delegator address or validator address |  |
| 500 | Internal Server Error |  |

### /staking/delegators/{delegatorAddr}/txs

#### GET
##### Summary:

Get all staking txs (i.e msgs) from a delegator

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| delegatorAddr | path | Bech32 AccAddress of Delegator | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [ [TxQuery](#txquery) ] |
| 204 | No staking transaction about this delegator address |  |
| 400 | Invalid delegator address |  |
| 500 | Internal Server Error |  |

### /staking/validators

#### GET
##### Summary:

Get all validator candidates. By default it returns only the bonded validators.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| status | query | The validator bond status. Must be either 'bonded', 'unbonded', or 'unbonding'. | No | string |
| page | query | The page number. | No | integer |
| limit | query | The maximum number of items per page. | No | integer |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [ [Validator](#validator) ] |
| 500 | Internal Server Error |  |

### /staking/validators/{validatorAddr}

#### GET
##### Summary:

Query the information from a single validator

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| validatorAddr | path | Bech32 OperatorAddress of validator | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Validator](#validator) |
| 400 | Invalid validator address |  |
| 500 | Internal Server Error |  |

### /staking/validators/{validatorAddr}/delegations

#### GET
##### Summary:

Get all delegations from a validator

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| validatorAddr | path | Bech32 OperatorAddress of validator | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [ [Delegation](#delegation) ] |
| 400 | Invalid validator address |  |
| 500 | Internal Server Error |  |

### /staking/validators/{validatorAddr}/unbonding_delegations

#### GET
##### Summary:

Get all unbonding delegations from a validator

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| validatorAddr | path | Bech32 OperatorAddress of validator | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [ [UnbondingDelegation](#unbondingdelegation) ] |
| 400 | Invalid validator address |  |
| 500 | Internal Server Error |  |

### /staking/pool

#### GET
##### Summary:

Get the current state of the staking pool

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | object |
| 500 | Internal Server Error |  |

### /staking/parameters

#### GET
##### Summary:

Get the current staking parameter values

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | object |
| 500 | Internal Server Error |  |

### /slashing/validators/{validatorPubKey}/signing_info

#### GET
##### Summary:

Get sign info of given validator

##### Description:

Get sign info of given validator

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| validatorPubKey | path | Bech32 validator public key | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [SigningInfo](#signinginfo) |
| 204 | No sign info of this validator |  |
| 400 | Invalid validator public key |  |
| 500 | Internal Server Error |  |

### /slashing/signing_infos

#### GET
##### Summary:

Get sign info of given all validators

##### Description:

Get sign info of all validators

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| page | query | Page number | Yes | integer |
| limit | query | Maximum number of items per page | Yes | integer |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [ [SigningInfo](#signinginfo) ] |
| 204 | No validators with sign info |  |
| 400 | Invalid validator public key for one of the validators |  |
| 500 | Internal Server Error |  |

### /slashing/validators/{validatorAddr}/unjail

#### POST
##### Summary:

Unjail a jailed validator

##### Description:

Send transaction to unjail a jailed validator

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| validatorAddr | path | Bech32 validator address | Yes | string |
| UnjailBody | body |  | Yes | object |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Tx was succesfully generated | [BroadcastTxCommitResult](#broadcasttxcommitresult) |
| 400 | Invalid validator address or base_req |  |
| 500 | Internal Server Error |  |

### /slashing/parameters

#### GET
##### Summary:

Get the current slashing parameters

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | object |
| 500 | Internal Server Error |  |

### /gov/proposals

#### POST
##### Summary:

Submit a proposal

##### Description:

Send transaction to submit a proposal

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| post_proposal_body | body | valid value of `"proposal_type"` can be `"text"`, `"parameter_change"`, `"software_upgrade"` | Yes | object |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Tx was succesfully generated | [StdTx](#stdtx) |
| 400 | Invalid proposal body |  |
| 500 | Internal Server Error |  |

#### GET
##### Summary:

Query proposals

##### Description:

Query proposals information with parameters

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| voter | query | voter address | No | string |
| depositor | query | depositor address | No | string |
| status | query | proposal status, valid values can be `"deposit_period"`, `"voting_period"`, `"passed"`, `"rejected"` | No | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [ [TextProposal](#textproposal) ] |
| 400 | Invalid query parameters |  |
| 500 | Internal Server Error |  |

### /gov/proposals/{proposalId}

#### GET
##### Summary:

Query a proposal

##### Description:

Query a proposal by id

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| proposalId | path |  | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [TextProposal](#textproposal) |
| 400 | Invalid proposal id |  |
| 500 | Internal Server Error |  |

### /gov/proposals/{proposalId}/proposer

#### GET
##### Summary:

Query proposer

##### Description:

Query for the proposer for a proposal

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| proposalId | path |  | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Proposer](#proposer) |
| 400 | Invalid proposal ID |  |
| 500 | Internal Server Error |  |

### /gov/proposals/{proposalId}/deposits

#### GET
##### Summary:

Query deposits

##### Description:

Query deposits by proposalId

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| proposalId | path |  | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [ [Deposit](#deposit) ] |
| 400 | Invalid proposal id |  |
| 500 | Internal Server Error |  |

#### POST
##### Summary:

Deposit tokens to a proposal

##### Description:

Send transaction to deposit tokens to a proposal

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| proposalId | path | proposal id | Yes | string |
| post_deposit_body | body |  | Yes | object |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [BroadcastTxCommitResult](#broadcasttxcommitresult) |
| 400 | Invalid proposal id or deposit body |  |
| 401 | Key password is wrong |  |
| 500 | Internal Server Error |  |

### /gov/proposals/{proposalId}/deposits/{depositor}

#### GET
##### Summary:

Query deposit

##### Description:

Query deposit by proposalId and depositor address

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| proposalId | path | proposal id | Yes | string |
| depositor | path | Bech32 depositor address | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Deposit](#deposit) |
| 400 | Invalid proposal id or depositor address |  |
| 404 | Found no deposit |  |
| 500 | Internal Server Error |  |

### /gov/proposals/{proposalId}/votes

#### GET
##### Summary:

Query voters

##### Description:

Query voters information by proposalId

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| proposalId | path | proposal id | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [ [Vote](#vote) ] |
| 400 | Invalid proposal id |  |
| 500 | Internal Server Error |  |

#### POST
##### Summary:

Vote a proposal

##### Description:

Send transaction to vote a proposal

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| proposalId | path | proposal id | Yes | string |
| post_vote_body | body | valid value of `"option"` field can be `"yes"`, `"no"`, `"no_with_veto"` and `"abstain"` | Yes | object |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [BroadcastTxCommitResult](#broadcasttxcommitresult) |
| 400 | Invalid proposal id or vote body |  |
| 401 | Key password is wrong |  |
| 500 | Internal Server Error |  |

### /gov/proposals/{proposalId}/votes/{voter}

#### GET
##### Summary:

Query vote

##### Description:

Query vote information by proposal Id and voter address

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| proposalId | path | proposal id | Yes | string |
| voter | path | Bech32 voter address | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Vote](#vote) |
| 400 | Invalid proposal id or voter address |  |
| 404 | Found no vote |  |
| 500 | Internal Server Error |  |

### /gov/proposals/{proposalId}/tally

#### GET
##### Summary:

Get a proposal's tally result at the current time

##### Description:

Gets a proposal's tally result at the current time. If the proposal is pending deposits (i.e status 'DepositPeriod') it returns an empty tally result.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| proposalId | path | proposal id | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [TallyResult](#tallyresult) |
| 400 | Invalid proposal id |  |
| 500 | Internal Server Error |  |

### /gov/parameters/deposit

#### GET
##### Summary:

Query governance deposit parameters

##### Description:

Query governance deposit parameters. The max_deposit_period units are in nanoseconds.

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | object |
| 400 | <other_path> is not a valid query request path |  |
| 404 | Found no deposit parameters |  |
| 500 | Internal Server Error |  |

### /gov/parameters/tallying

#### GET
##### Summary:

Query governance tally parameters

##### Description:

Query governance tally parameters

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK |  |
| 400 | <other_path> is not a valid query request path |  |
| 404 | Found no tally parameters |  |
| 500 | Internal Server Error |  |

### /gov/parameters/voting

#### GET
##### Summary:

Query governance voting parameters

##### Description:

Query governance voting parameters. The voting_period units are in nanoseconds.

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK |  |
| 400 | <other_path> is not a valid query request path |  |
| 404 | Found no voting parameters |  |
| 500 | Internal Server Error |  |

### /distribution/delegators/{delegatorAddr}/rewards

#### GET
##### Summary:

Get the total rewards balance from all delegations

##### Description:

Get the sum of all the rewards earned by delegations by a single delegator

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| delegatorAddr | path | Bech32 AccAddress of Delegator | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [ [Coin](#coin) ] |
| 400 | Invalid delegator address |  |
| 500 | Internal Server Error |  |

#### POST
##### Summary:

Withdraw all the delegator's delegation rewards

##### Description:

Withdraw all the delegator's delegation rewards

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| delegatorAddr | path | Bech32 AccAddress of Delegator | Yes | string |
| Withdraw request body | body |  | No |  |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [BroadcastTxCommitResult](#broadcasttxcommitresult) |
| 400 | Invalid delegator address |  |
| 401 | Key password is wrong |  |
| 500 | Internal Server Error |  |

### /distribution/delegators/{delegatorAddr}/rewards/{validatorAddr}

#### GET
##### Summary:

Query a delegation reward

##### Description:

Query a single delegation reward by a delegator

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| delegatorAddr | path | Bech32 AccAddress of Delegator | Yes | string |
| validatorAddr | path | Bech32 OperatorAddress of validator | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [ [Coin](#coin) ] |
| 400 | Invalid delegator address |  |
| 500 | Internal Server Error |  |

#### POST
##### Summary:

Withdraw a delegation reward

##### Description:

Withdraw a delegator's delegation reward from a single validator

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| delegatorAddr | path | Bech32 AccAddress of Delegator | Yes | string |
| validatorAddr | path | Bech32 OperatorAddress of validator | Yes | string |
| Withdraw request body | body |  | No |  |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [BroadcastTxCommitResult](#broadcasttxcommitresult) |
| 400 | Invalid delegator address or delegation body |  |
| 401 | Key password is wrong |  |
| 500 | Internal Server Error |  |

### /distribution/delegators/{delegatorAddr}/withdraw_address

#### GET
##### Summary:

Get the rewards withdrawal address

##### Description:

Get the delegations' rewards withdrawal address. This is the address in which the user will receive the reward funds

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| delegatorAddr | path | Bech32 AccAddress of Delegator | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [Address](#address) |
| 400 | Invalid delegator address |  |
| 500 | Internal Server Error |  |

#### POST
##### Summary:

Replace the rewards withdrawal address

##### Description:

Replace the delegations' rewards withdrawal address for a new one.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| delegatorAddr | path | Bech32 AccAddress of Delegator | Yes | string |
| Withdraw request body | body |  | No |  |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [BroadcastTxCommitResult](#broadcasttxcommitresult) |
| 400 | Invalid delegator or withdraw address |  |
| 401 | Key password is wrong |  |
| 500 | Internal Server Error |  |

### /distribution/validators/{validatorAddr}

#### GET
##### Summary:

Validator distribution information

##### Description:

Query the distribution information of a single validator

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| validatorAddr | path | Bech32 OperatorAddress of validator | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [ValidatorDistInfo](#validatordistinfo) |
| 400 | Invalid validator address |  |
| 500 | Internal Server Error |  |

### /distribution/validators/{validatorAddr}/outstanding_rewards

#### GET
##### Summary:

Fee distribution outstanding rewards of a single validator

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| validatorAddr | path | Bech32 OperatorAddress of validator | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [ [Coin](#coin) ] |
| 500 | Internal Server Error |  |

### /distribution/validators/{validatorAddr}/rewards

#### GET
##### Summary:

Commission and self-delegation rewards of a single validator

##### Description:

Query the commission and self-delegation rewards of validator.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| validatorAddr | path | Bech32 OperatorAddress of validator | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [ [Coin](#coin) ] |
| 400 | Invalid validator address |  |
| 500 | Internal Server Error |  |

#### POST
##### Summary:

Withdraw the validator's rewards

##### Description:

Withdraw the validator's self-delegation and commissions rewards

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| validatorAddr | path | Bech32 OperatorAddress of validator | Yes | string |
| Withdraw request body | body |  | No |  |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [BroadcastTxCommitResult](#broadcasttxcommitresult) |
| 400 | Invalid validator address |  |
| 401 | Key password is wrong |  |
| 500 | Internal Server Error |  |

### /distribution/community_pool

#### GET
##### Summary:

Community pool parameters

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [ [Coin](#coin) ] |
| 500 | Internal Server Error |  |

### /distribution/parameters

#### GET
##### Summary:

Fee distribution parameters

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK |  |
| 500 | Internal Server Error |  |

### /minting/parameters

#### GET
##### Summary:

Minting module parameters

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK |  |
| 500 | Internal Server Error |  |

### /minting/inflation

#### GET
##### Summary:

Current minting inflation value

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | string |
| 500 | Internal Server Error |  |

### /minting/annual-provisions

#### GET
##### Summary:

Current minting annual provisions value

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | string |
| 500 | Internal Server Error |  |

### /interest/current

#### GET
##### Description:

Shows current interest set for specified denoms

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Returns the interest for a set denom |

### /csdts/params

#### GET
##### Description:

Retrieves the current accepted collateral and debt for CSDTS

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Returns the current accepted collateral and debt for CSDTS |

### /oracle/rawprices/uftm

#### GET
##### Description:

Retrieve the posted raw prices for a denom via the oracle

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Returns a list of all raw posted prices |

### /csdts

#### GET
##### Description:

Retrieve a specific csdt based on owner and denomination

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| owner | query |  | No | string |
| collateralDenom | query |  | No | string |
| underCollateralizedAt | query |  | No | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Auto generated using Swagger Inspector |

### /oracle/assets

#### GET
##### Description:

Show the current list of supported assets for the oracle

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | The list of assets accepted |

### /oracle/currentprice/uftm

#### GET
##### Description:

The current calculated median price for an asset

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | The median price |

### Models


#### node_info

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| node_info | object |  | No |
| application_version | object |  | No |

#### application_version

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| name | string |  | No |
| server_name | string |  | No |
| client_name | string |  | No |
| version | string |  | No |
| commit | string |  | No |
| build_tags | string |  | No |
| go | string |  | No |

#### CheckTxResult

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | integer |  | No |
| data | string |  | No |
| gas_used | integer |  | No |
| gas_wanted | integer |  | No |
| info | string |  | No |
| log | string |  | No |
| tags | [ [KVPair](#kvpair) ] |  | No |

#### DeliverTxResult

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | integer |  | No |
| data | string |  | No |
| gas_used | integer |  | No |
| gas_wanted | integer |  | No |
| info | string |  | No |
| log | string |  | No |
| tags | [ [KVPair](#kvpair) ] |  | No |

#### BroadcastTxCommitResult

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| check_tx | [CheckTxResult](#checktxresult) |  | No |
| deliver_tx | [DeliverTxResult](#delivertxresult) |  | No |
| hash | [Hash](#hash) |  | No |
| height | integer |  | No |

#### KVPair

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| key | string |  | No |
| value | string |  | No |

#### Msg

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| Msg | string |  |  |

#### Address

bech32 encoded address

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| Address | string | bech32 encoded address |  |

#### ValidatorAddress

bech32 encoded address

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| ValidatorAddress | string | bech32 encoded address |  |

#### Coin

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| denom | string |  | No |
| amount | string |  | No |

#### Hash

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| Hash | string |  |  |

#### TxQuery

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| hash | string |  | No |
| height | number |  | No |
| tx | [StdTx](#stdtx) |  | No |
| result | object |  | No |

#### StdTx

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| msg | [ [Msg](#msg) ] |  | No |
| fee | object |  | No |
| memo | string |  | No |
| signature | object |  | No |

#### KeyOutput

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| name | string |  | No |
| address | string |  | No |
| pub_key | string |  | No |
| type | string |  | No |
| seed | string |  | No |

#### BlockID

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| hash | [Hash](#hash) |  | No |
| parts | object |  | No |

#### BlockHeader

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| chain_id | string |  | No |
| height | number |  | No |
| time | string |  | No |
| num_txs | number |  | No |
| last_block_id | [BlockID](#blockid) |  | No |
| total_txs | number |  | No |
| last_commit_hash | [Hash](#hash) |  | No |
| data_hash | [Hash](#hash) |  | No |
| validators_hash | [Hash](#hash) |  | No |
| next_validators_hash | [Hash](#hash) |  | No |
| consensus_hash | [Hash](#hash) |  | No |
| app_hash | [Hash](#hash) |  | No |
| last_results_hash | [Hash](#hash) |  | No |
| evidence_hash | [Hash](#hash) |  | No |
| proposer_address | [Address](#address) |  | No |
| version | object |  | No |

#### Block

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| header | [BlockHeader](#blockheader) |  | No |
| txs | [ string ] |  | No |
| evidence | [ string ] |  | No |
| last_commit | object |  | No |

#### BlockQuery

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| block_meta | object |  | No |
| block | [Block](#block) |  | No |

#### BaseReq

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| from | string | Sender address or Keybase name to generate a transaction | No |
| memo | string |  | No |
| chain_id | string |  | No |
| account_number | string |  | No |
| sequence | string |  | No |
| gas | string |  | No |
| gas_adjustment | string |  | No |
| fees | [ [Coin](#coin) ] |  | No |
| simulate | boolean | Estimate gas for a transaction (cannot be used in conjunction with generate_only) | No |

#### TendermintValidator

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| address | [ValidatorAddress](#validatoraddress) |  | No |
| pub_key | string |  | No |
| voting_power | string |  | No |
| proposer_priority | string |  | No |

#### TextProposal

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| proposal_id | integer |  | No |
| title | string |  | No |
| description | string |  | No |
| proposal_type | string |  | No |
| proposal_status | string |  | No |
| final_tally_result | [TallyResult](#tallyresult) |  | No |
| submit_time | string |  | No |
| total_deposit | [ [Coin](#coin) ] |  | No |
| voting_start_time | string |  | No |

#### Proposer

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| proposal_id | integer |  | No |
| proposer | string |  | No |

#### Deposit

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| amount | [ [Coin](#coin) ] |  | No |
| proposal_id | integer |  | No |
| depositor | [Address](#address) |  | No |

#### TallyResult

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| yes | string |  | No |
| abstain | string |  | No |
| no | string |  | No |
| no_with_veto | string |  | No |

#### Vote

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| voter | string |  | No |
| proposal_id | integer |  | No |
| option | string |  | No |

#### Validator

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| operator_address | [ValidatorAddress](#validatoraddress) |  | No |
| consensus_pubkey | string |  | No |
| jailed | boolean |  | No |
| status | integer |  | No |
| tokens | string |  | No |
| delegator_shares | string |  | No |
| description | object |  | No |
| bond_height | string |  | No |
| bond_intra_tx_counter | integer |  | No |
| unbonding_height | string |  | No |
| unbonding_time | string |  | No |
| commission | object |  | No |

#### Delegation

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| delegator_address | string |  | No |
| validator_address | string |  | No |
| shares | string |  | No |
| height | integer |  | No |

#### UnbondingDelegation

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| delegator_address | string |  | No |
| validator_address | string |  | No |
| initial_balance | string |  | No |
| balance | string |  | No |
| creation_height | integer |  | No |
| min_time | integer |  | No |

#### Redelegation

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| delegator_address | string |  | No |
| validator_src_address | string |  | No |
| validator_dst_address | string |  | No |
| creation_height | integer |  | No |
| min_time | integer |  | No |
| initial_balance | string |  | No |
| balance | string |  | No |
| shares_src | string |  | No |
| shares_dst | string |  | No |

#### ValidatorDistInfo

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| operator_address | [ValidatorAddress](#validatoraddress) |  | No |
| self_bond_rewards | [ [Coin](#coin) ] |  | No |
| val_commission | [ [Coin](#coin) ] |  | No |

#### SigningInfo

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| start_height | string |  | No |
| index_offset | string |  | No |
| jailed_until | string |  | No |
| missed_blocks_counter | string |  | No |

#### sync

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| syncing | boolean |  | No |

#### block_meta

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| block_id | object |  | No |
| header | object |  | No |

#### block_query

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| block_meta | object |  | No |
| block | object |  | No |

#### validator_set

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| height | string |  | No |
| result | object |  | No |

#### tx

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| height | string |  | No |
| txhash | string |  | No |
| raw_log | string |  | No |
| logs | [ object ] |  | No |
| gas_wanted | string |  | No |
| gas_used | string |  | No |
| tx | object |  | No |
| timestamp | dateTime |  | No |
| events | [ object ] |  | No |

#### balances

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| height | string |  | No |
| result | [ object ] |  | No |

#### accounts

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| height | string |  | No |
| result | object |  | No |

#### BlockInclusionResponse

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| block_inclusion | [BlockInclusionResponse_block_inclusion](#blockinclusionresponse_block_inclusion) |  | No |

#### BlockInclusionFailure

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | [BlockInclusionFailure_error](#blockinclusionfailure_error) |  | No |

#### BatchesResponse

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| block_inclusion | [BlockInclusionResponse_block_inclusion](#blockinclusionresponse_block_inclusion) |  | No |
| price | string |  | No |
| amount | string |  | No |

#### BatchInfo

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| price | string |  | No |
| amount | string |  | No |

#### OrderCreationRequest

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| market_id | string |  | No |
| direction | [Direction](#direction) |  | No |
| price | string |  | No |
| quantity | string |  | No |
| type | [Type](#type) |  | No |
| time_in_force | integer |  | No |

#### OrderCreationResponse

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| block_inclusion | [BlockInclusionResponse_block_inclusion](#blockinclusionresponse_block_inclusion) |  | No |
| id | string |  | No |
| market_id | string |  | No |
| direction | [Direction](#direction) |  | No |
| price | string |  | No |
| quantity | string |  | No |
| status | [Status](#status) |  | No |
| type | [Type](#type) |  | No |
| time_in_force | integer |  | No |

#### Order

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| market_id | string |  | No |
| direction | [Direction](#direction) |  | No |
| price | string |  | No |
| quantity | string |  | No |
| status | [Status](#status) |  | No |
| type | [Type](#type) |  | No |
| time_in_force | integer |  | No |

#### OrderWithFills

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| OrderWithFills |  |  |  |

#### Balance

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| balances | [ [Balance_balances](#balance_balances) ] |  | No |

#### Fill

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| Fill |  |  |  |

#### CandlestickResponse

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| market_id | string |  | No |
| candles | [ [CandlestickResponse_candles](#candlestickresponse_candles) ] |  | No |

#### Spread

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| block_number | string |  | No |
| market_id | string |  | No |
| bids | [ [PriceQuantity](#pricequantity) ] |  | No |
| asks | [ [PriceQuantity](#pricequantity) ] |  | No |

#### PriceQuantity

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| price | string |  | No |
| quantity | string |  | No |

#### Market

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| pair | string |  | No |
| base_asset_id | string |  | No |
| quote_asset_id | string |  | No |

#### Withdrawal

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| beneficiary | string | The address of the recipient who will unlock funds on the remote chain. Hex-encoded. | No |
| merkle_proof | string | The Merkle proof required to unlock funds on the relay chain. | No |
| merkle_leaf | string | The Merkle leaf hash of the withdrawal. | No |
| asset_id | string | The ID of the cleared asset to be withdrawn. | No |
| burn_id | string | The ID of the underlying burn used to initiate this withdrawal. | No |
| quantity | string | The amount of the cleared asset to withdraw, as represented in the asset's base units. | No |
| initiated_block | double | The block number when this withdrawal was initiated. | No |
| owner | string | The address whose funds are being withdrawn. | No |

#### body

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| username | string |  | No |
| password | string |  | No |

#### body_1

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| old_password | string |  | No |
| new_password | string |  | No |

#### body_2

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| order_ids | [ string ] |  | No |

#### inline_response_200

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| next_id | string |  | No |
| orders | [ [OrderWithFills](#orderwithfills) ] |  | No |

#### inline_response_200_1

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| fills | [ [Fill](#fill) ] |  | No |

#### body_3

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| to | string |  | No |
| amount | string |  | No |
| asset_id | string |  | No |

#### inline_response_200_2

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| owner | string |  | No |
| withdrawals | [ [Withdrawal](#withdrawal) ] |  | No |

#### body_4

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| beneficiary | string | The address of the recipient who will unlock funds on the relay chain. Hex-encoded. | No |
| asset_id | string | The ID of the cleared asset to be withdrawn. | No |
| quantity | string | The amount of the cleared asset to withdraw, as represented in the asset's base units. | No |

#### body_5

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| asset_id | string | The asset ID deposited. | No |
| quantity | string | The amount of the asset deposited. | No |
| relay_chain_id | [RelayChainId](#relaychainid) |  | No |
| relay_chain_transaction_hash | string | The transaction hash of the deposit on the relay chain. | No |

#### inline_response_200_3

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| pair | string |  | No |
| volume | string |  | No |
| change | string |  | No |
| last | string |  | No |
| high | string |  | No |
| low | string |  | No |

#### BlockInclusionResponse_block_inclusion

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| block_number | string |  | No |
| transaction_hash | string |  | No |
| block_timestamp | double |  | No |

#### BlockInclusionFailure_error

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| codespace | integer |  | No |
| code | integer |  | No |

#### Balance_balances

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| asset_id | string |  | No |
| name | string |  | No |
| symbol | string |  | No |
| liquid | string | Amount of this asset available for trading. | No |
| at_risk | string | Amount of this asset current on the order book. | No |

#### CandlestickResponse_candles

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| date | string | ISO8601 | No |
| open | string |  | No |
| close | string |  | No |
| high | string |  | No |
| low | string |  | No |

#### Direction

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| Direction | string |  |  |

#### granularity

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| granularity | string |  |  |

#### RelayChainId

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| RelayChainId | string |  |  |

#### Status

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| Status | string |  |  |

#### Type

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| Type | string |  |  |