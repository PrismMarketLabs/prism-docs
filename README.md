# Prism Protocol Documentation

## Smart contract address

Prism smart contract is deployed at:

**testnet**

`0.0.9159758` (latest)

`0.0.9070333`

`0.0.8947052`

`0.0.8946970`

**mainnet**

`TBC`

## API endpoints (prod)

`https://previewnet.prism.market`

`https://testnet.prism.market`

`https://prism.market` (mainnet)

## API interface

API protobuf interface

```proto
syntax = "proto3";

package api;
option go_package = "api/gen;api";

import "validate/validate.proto"; // PGV

service ApiServicePublic {
  rpc Health(Empty) returns (StdResponse);
  rpc NewsLetter(NewsLetterRequest) returns (StdResponse);
  rpc CreatePredictionIntent(PrismPredictionIntentRequest) returns (StdResponse);
  rpc GetMarketById(MarketIdRequest) returns (MarketResponse);
  rpc GetMarkets(LimitOffsetRequest) returns (MarketsResponse);  
  rpc PriceHistory(PriceHistoryRequest) returns (PriceHistoryResponse);
  rpc MacroMetadata(Empty) returns (MacroMetadataResponse); // general market data - volume, nMarkets, TVL, liquidity, etc.
  rpc CreateComment(CreateCommentRequest) returns (CreateCommentResponse);
  rpc GetComments(GetCommentsRequest) returns (GetCommentsResponse);
  rpc GetUserPortfolio(UserPortfolioRequest) returns (UserPortfolioResponse);
  rpc CancelPredictionIntent(CancelOrderRequest) returns (StdResponse);
}


/////
// Common
/////

message Empty {}

message StdResponse {
  string message = 1     [json_name = "message"];
  int32 error_code = 2   [json_name = "errorCode"];
}

message LimitOffsetRequest {
  int32 limit = 1  [(validate.rules).int32 = {gt: 0}];
  int32 offset = 2 [(validate.rules).int32 = {gte: 0}];
}

message MarketIdRequest {
  string market_id = 1 [json_name = "marketId",     (validate.rules).string = {pattern: "(?i)^[0-9a-f]{8}-[0-9a-f]{4}-7[0-9a-f]{3}-[89ab][0-9a-f]{3}-[0-9a-f]{12}$"} /* Strict RFC-9562-compliant UUIDv7 */];
  optional string lang = 2;
}

/////
// ApiServicePublic
////

/////
// Common
/////

message Empty {}

message StdResponse {
  string message = 1     [json_name = "message"];
  int32 error_code = 2   [json_name = "errorCode"];
}

message LimitOffsetRequest {
  int32 limit = 1  [(validate.rules).int32 = {gt: 0}];
  int32 offset = 2 [(validate.rules).int32 = {gte: 0}];
}

message MarketIdRequest {
  string market_id = 1 [json_name = "marketId",     (validate.rules).string = {pattern: "(?i)^[0-9a-f]{8}-[0-9a-f]{4}-7[0-9a-f]{3}-[89ab][0-9a-f]{3}-[0-9a-f]{12}$"} /* Strict RFC-9562-compliant UUIDv7 */];
  optional string lang = 2;
}

/////
// ApiServicePublic
////

message PrismPredictionIntentRequest {
  string tx_id = 1              [json_name = "txId",        (validate.rules).string = {pattern: "(?i)^[0-9a-f]{8}-[0-9a-f]{4}-7[0-9a-f]{3}-[89ab][0-9a-f]{3}-[0-9a-f]{12}$"} /* Strict RFC-9562-compliant UUIDv7 */];
  string net = 2                [json_name = "net",         (validate.rules).string = {in: ["mainnet", "testnet", "previewnet"]} /* Hedera network */];
  string market_id = 3          [json_name = "marketId",    (validate.rules).string = {pattern: "(?i)^[0-9a-f]{8}-[0-9a-f]{4}-7[0-9a-f]{3}-[89ab][0-9a-f]{3}-[0-9a-f]{12}$"} /* Strict RFC-9562-compliant UUIDv7 */];
  string generated_at = 4       [json_name = "generatedAt", (validate.rules).string = {pattern: "^\\d{4}-(0[1-9]|1[0-2])-(0[1-9]|[12]\\d|3[01])T([01]\\d|2[0-3]):[0-5]\\d:[0-5]\\d\\.\\d{3}Z$"} /* UTC ISO 8601 (Zulu time only) */];
  string account_id = 5         [json_name = "accountId",   (validate.rules).string = {pattern: "^(0|[1-9]\\d*)\\.(0|[1-9]\\d*)\\.(0|[1-9]\\d*)$"} /* Hedera account ID (no leading zeros) */];
  double price_usd = 6          [json_name = "priceUsd",    (validate.rules).double = {gt: -1.0, lt: 1.0} /* price_usd <0 => sell, price_usd >=0 => buy */];
  double qty = 7                [json_name = "qty",         (validate.rules).double = {gt: 0.0}];
  string sig = 8                [json_name = "sig",         (validate.rules).string = {pattern: "^[A-Za-z0-9+/]{20,100}={0,2}$"} /* base64-encoded signature (URL-safe base64 without padding, min 20 chars, max 100 chars) */];
  // pass extra key info - i) avoid lookups ii) handle situation where user has changed their key
  string public_key = 9         [json_name = "publicKey",   (validate.rules).string = {pattern: "^(04[0-9a-fA-F]{128}|0[23][0-9a-fA-F]{64}|[0-9a-fA-F]{64})$"} /* ECDSA (compressed/uncompressed) or Ed25519 public key in hex format, no 0x prefix */];
  string evm_address = 10       [json_name = "evmAddress",  (validate.rules).string = {pattern: "^[0-9a-fA-F]{40}$"} /* 20-byte (40 hex chars) EVM address (no 0x prefix) */];
  uint32 key_type = 11          [json_name = "keyType",     (validate.rules).uint32 = {in: [1, 2]} /* 1 = ed25519, 2 = ecdsa_secp256k1 */];
  string primary_secondary = 12 [json_name = "primarySecondary", (validate.rules).string = {in: ["p", "s"]}];
}

message Category {
  int32 id = 1 [json_name = "id"];
  string name = 2 [json_name = "name"];
}

message UnixDateRange {
  int32 start = 1;
  int32 end = 2;
}

message MacroMetadataResponse {
  repeated string available_networks = 1              [json_name = "availableNetworks"];
  repeated string available_networks_admin = 2        [json_name = "availableNetworksAdmin"];
  map<string, string> smart_contract_ids = 3          [json_name = "smartContractIds"];
  map<string, string> usdc_token_ids = 4              [json_name = "usdcTokenIds"];
  uint32 usdc_decimals = 5                            [json_name = "usdcDecimals"];
  uint64 market_creation_fee_scaled_usdc = 6          [json_name = "marketCreationFeeScaledUsdc"];
  uint32 n_markets = 7                                [json_name = "nMarkets"];
  map<string, string> token_ids = 8                   [json_name = "tokenIds"];
  double min_order_size_usd = 9                       [json_name = "minOrderSizeUsd"];
  double tv_pending_usd = 10                          [json_name = "tvPendingUsd"];
  double tv_matched_usd = 11                          [json_name = "tvMatchedUsd"];
  double tvl_usd = 12                                 [json_name = "tvlUsd"];
  map<string, double> total_volume_usd = 13           [json_name = "totalVolumeUsd"];
  uint32 active_traders = 14                          [json_name = "activeTraders"];
  repeated Category categories = 15                   [json_name = "categories"];
  // constants.go/SigSchemeDateRanges
  repeated UnixDateRange sig_scheme_date_ranges = 16  [json_name = "sigSchemeDateRanges"];
}

message NewsLetterRequest {
  string email = 1 [json_name = "email", (validate.rules).string = {email: true}];
}

message UserPortfolioRequest {
  string evm_address = 1           [json_name = "evmAddress",  (validate.rules).string = {pattern: "^[0-9a-fA-F]{40}$"} /* 20-byte (40 hex chars) EVM address (no 0x prefix) */];
  string net = 2                   [json_name = "net",         (validate.rules).string = {in: ["mainnet", "testnet", "previewnet"]} /* Hedera network */];
  optional string market_id = 3    [json_name = "marketId",    (validate.rules).string = {pattern: "(?i)^[0-9a-f]{8}-[0-9a-f]{4}-7[0-9a-f]{3}-[89ab][0-9a-f]{3}-[0-9a-f]{12}$"} /* Strict RFC-9562-compliant UUIDv7 */];
}

message PredictionIntentResponse {
  string tx_id = 1              [json_name = "txId",        (validate.rules).string = {pattern: "(?i)^[0-9a-f]{8}-[0-9a-f]{4}-7[0-9a-f]{3}-[89ab][0-9a-f]{3}-[0-9a-f]{12}$"} /* Strict RFC-9562-compliant UUIDv7 */];
  string net = 2                [json_name = "net",         (validate.rules).string = {in: ["mainnet", "testnet", "previewnet"]} /* Hedera network */];
  string market_id = 3          [json_name = "marketId",    (validate.rules).string = {pattern: "(?i)^[0-9a-f]{8}-[0-9a-f]{4}-7[0-9a-f]{3}-[89ab][0-9a-f]{3}-[0-9a-f]{12}$"} /* Strict RFC-9562-compliant UUIDv7 */];
  string generated_at = 4       [json_name = "generatedAt", (validate.rules).string = {pattern: "^\\d{4}-(0[1-9]|1[0-2])-(0[1-9]|[12]\\d|3[01])T([01]\\d|2[0-3]):[0-5]\\d:[0-5]\\d\\.\\d{3}Z$"} /* UTC ISO 8601 (Zulu time only) */];
  string account_id = 5         [json_name = "accountId",   (validate.rules).string = {pattern: "^(0|[1-9]\\d*)\\.(0|[1-9]\\d*)\\.(0|[1-9]\\d*)$"} /* Hedera account ID (no leading zeros) */];
  double price_usd = 6          [json_name = "priceUsd",    (validate.rules).double = {gt: -1.0, lt: 1.0} /* price_usd <0 => sell, price_usd >=0 => buy */];
  double qty = 7                [json_name = "qty",         (validate.rules).double = {gt: 0.0}];
  string primary_secondary = 8  [json_name = "primarySecondary", (validate.rules).string = {in: ["p", "s"]}];
}

message PredictionIntents {
  repeated PredictionIntentResponse prediction_intents = 1   [json_name = "openPredictionIntents"];
}

message Position {
  string market_id = 1        [json_name = "marketId"];
  string evm_address = 2      [json_name = "evmAddress"];
  uint64 yes = 3              [json_name = "yes"];
  uint64 no = 4               [json_name = "no"];
  string updated_at = 5      [json_name = "updatedAt"];
  string created_at = 6      [json_name = "createdAt"];
}

message PositionInfo {
  Position position = 1         [json_name = "position"];
  float price_usd = 2           [json_name = "priceUsd"];
  bool is_paused = 3            [json_name = "isPaused"];
  string resolved_at = 4        [json_name = "resolvedAt"];
  string redeemed_at = 5        [json_name = "redeemedAt"];
}

message PrismPoints {
  uint32 season_id = 1          [json_name = "seasonId"];
  float points = 2              [json_name = "points"];
}

message UserPortfolioResponse {
  map<string, PositionInfo> positions = 1                      [json_name = "positions"];
  map<string, PredictionIntents> open_prediction_intents = 2   [json_name = "openPredictionIntents"];
  repeated PrismPoints prism_points = 3                        [json_name = "prismPoints"];
  uint64 prism_token_balance = 4                               [json_name = "prismTokenBalance"];
}

message MarketResponse {
  string market_id = 1             [json_name = "marketId"];
  string net = 2                   [json_name = "net"];
  string statement = 3             [json_name = "statement"];
  bool is_paused = 4               [json_name = "isPaused"];
  bool is_suspended = 5            [json_name = "isSuspended"];
  string created_at = 6            [json_name = "createdAt"];
  string resolved_at = 7           [json_name = "resolvedAt"];
  string image_url = 8             [json_name = "imageUrl"];
  float price_usd = 9              [json_name = "priceUsd"];
  // string smart_contract_id = 9  [json_name = "smartContractId"]; // not needed - smart_contract_id is a column in the markets table
  string description = 10          [json_name = "description"];
  string closes_at = 11            [json_name = "closesAt"];
  optional bool outcome = 12       [json_name = "outcome"];
  string smart_contract_id = 13    [json_name = "smartContractId"];
  repeated int32 category_ids = 14 [json_name = "categoryIds"];
  string alias_yes = 15            [json_name = "aliasYes"];
  string alias_no = 16             [json_name = "aliasNo"];
  string hex_color_yes = 17        [json_name = "hexColorYes"];
  string hex_color_no = 18         [json_name = "hexColorNo"];
}

message MarketsResponse {
  repeated MarketResponse markets = 1;
}

message PriceHistoryRequest {
  string market_id = 1    [json_name = "marketId", (validate.rules).string = {pattern: "(?i)^[0-9a-f]{8}-[0-9a-f]{4}-7[0-9a-f]{3}-[89ab][0-9a-f]{3}-[0-9a-f]{12}$"} /* Strict RFC-9562-compliant UUIDv7 */];
  string net = 2          [json_name = "net",      (validate.rules).string = {in: ["mainnet", "testnet", "previewnet"]} /* Hedera network */];
  string resolution = 3   [json_name = "resolution",      (validate.rules).string = {in: ["second", "minute", "hour", "day", "week", "month", "quarter", "year", "decade"]} /* zoom levels: postgres truncation */];
  string from = 4         [json_name = "from", (validate.rules).string = {pattern: "^\\d{4}-(0[1-9]|1[0-2])-(0[1-9]|[12]\\d|3[01])T([01]\\d|2[0-3]):[0-5]\\d:[0-5]\\d\\.\\d{3}Z$"} /* UTC ISO 8601 (Zulu time only) */];
  string to = 5           [json_name = "to", (validate.rules).string = {pattern: "^\\d{4}-(0[1-9]|1[0-2])-(0[1-9]|[12]\\d|3[01])T([01]\\d|2[0-3]):[0-5]\\d:[0-5]\\d\\.\\d{3}Z$"} /* UTC ISO 8601 (Zulu time only) */];
  optional int32 limit = 6         [json_name = "limit",     (validate.rules).int32 = {gt: 0, lte: 1000} /* max 1000 ticks per request */];
  optional int32 offset = 7        [json_name = "offset",    (validate.rules).int32 = {gte: 0} /* offset in ticks */];
}

message PriceHistoryResponse { // want [timestampMs[], priceUsd[]] for graphing (e.g. uplot)
  repeated uint64 timestamp_ms = 1   [json_name = "timestampMs"];
  repeated float price_usd = 2       [json_name = "priceUsd"];
}

message GetCommentsRequest {
  string market_id = 1      [json_name = "marketId",  (validate.rules).string = {pattern: "(?i)^[0-9a-f]{8}-[0-9a-f]{4}-7[0-9a-f]{3}-[89ab][0-9a-f]{3}-[0-9a-f]{12}$"} /* Strict RFC-9562-compliant UUIDv7 */];
  optional int32 limit = 2  [json_name = "limit",     (validate.rules).int32 = {gt: 0, lte: 100} /* max 100 comments per request */];
  optional int32 offset = 3 [json_name = "offset",    (validate.rules).int32 = {gte: 0} /* offset in comments */];
}

message Comment {
  // string comment_id = 1    [json_name = "commentId"];
  string account_id = 1    [json_name = "accountId"];
  string content = 2       [json_name = "content"];
  string sig = 3           [json_name = "sig"];
  string public_key = 4    [json_name = "publicKey"];
  uint32 key_type = 5      [json_name = "keyType"];
  string created_at = 6    [json_name = "createdAt"];
}

message CreateCommentResponse {
  Comment comment = 1;
}

message GetCommentsResponse {
  repeated Comment comments = 1;
}

message CreateCommentRequest {
  string market_id = 1    [json_name = "marketId",    (validate.rules).string = {pattern: "(?i)^[0-9a-f]{8}-[0-9a-f]{4}-7[0-9a-f]{3}-[89ab][0-9a-f]{3}-[0-9a-f]{12}$"} /* Strict RFC-9562-compliant UUIDv7 */];
  string account_id = 2   [json_name = "accountId",   (validate.rules).string = {pattern: "^(0|[1-9]\\d*)\\.(0|[1-9]\\d*)\\.(0|[1-9]\\d*)$"} /* Hedera account ID (no leading zeros) */];
  string content = 3      [json_name = "content",     (validate.rules).string = {min_len: 1, max_len: 1000}];
  string sig = 4          [json_name = "sig",         (validate.rules).string = {pattern: "^[A-Za-z0-9+/]{20,100}={0,2}$"} /* base64-encoded signature (URL-safe base64 without padding, min 20 chars, max 100 chars) */];
  string public_key = 5   [json_name = "publicKey",   (validate.rules).string = {pattern: "^(04|03|02)[0-9a-fA-F]{32,256}$"} /* uncompressed (04...) or compressed (02... or 03...) public key (ed25519, ecdsa, etc.) in hex format */];
  uint32 key_type = 6     [json_name = "keyType",     (validate.rules).uint32 = {in: [1, 2]} /* 1 = ed25519, 2 = ecdsa_secp256k1 */];
}

message CancelOrderRequest {
  string market_id = 1      [json_name = "marketId",  (validate.rules).string = {pattern: "(?i)^[0-9a-f]{8}-[0-9a-f]{4}-7[0-9a-f]{3}-[89ab][0-9a-f]{3}-[0-9a-f]{12}$"} /* Strict RFC-9562-compliant UUIDv7 */];
  string tx_id = 2          [json_name = "txId",      (validate.rules).string = {pattern: "(?i)^[0-9a-f]{8}-[0-9a-f]{4}-7[0-9a-f]{3}-[89ab][0-9a-f]{3}-[0-9a-f]{12}$"} /* Strict RFC-9562-compliant UUIDv7 */];
}
```

## ABI

Application Binary Interface

```json

testnet:0.0.9159758

[{"inputs":[{"internalType":"address","name":"_collateralToken","type":"address"}],"stateMutability":"nonpayable","type":"constructor"},{"anonymous":false,"inputs":[{"indexed":false,"internalType":"uint128","name":"marketId","type":"uint128"},{"indexed":false,"internalType":"bool","name":"outcome","type":"bool"}],"name":"MarketResolved","type":"event"},{"anonymous":false,"inputs":[{"indexed":false,"internalType":"uint128","name":"marketId","type":"uint128"},{"indexed":true,"internalType":"address","name":"buyer","type":"address"},{"indexed":false,"internalType":"uint256","name":"collateralUsd","type":"uint256"},{"indexed":false,"internalType":"uint256","name":"qtyScaled","type":"uint256"},{"indexed":false,"internalType":"bool","name":"primarySecondary","type":"bool"}],"name":"PositionTokensPurchased","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"internalType":"address","name":"token","type":"address"}],"name":"TokenAssociated","type":"event"},{"anonymous":false,"inputs":[{"indexed":false,"internalType":"uint128","name":"marketId","type":"uint128"},{"indexed":true,"internalType":"address","name":"winner","type":"address"},{"indexed":false,"internalType":"uint256","name":"amount","type":"uint256"}],"name":"WinningsRedeemed","type":"event"},{"inputs":[{"internalType":"address","name":"tokenAddress","type":"address"}],"name":"associateToken","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address","name":"","type":"address"}],"name":"associatedTokens","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"}],"name":"claimCollateralAfterOneYear","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[],"name":"collateralToken","outputs":[{"internalType":"contract IERC20","name":"","type":"address"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"collateralTokenNdecimals","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"},{"internalType":"string","name":"_statement","type":"string"}],"name":"createNewMarket","outputs":[{"internalType":"uint256","name":"allowance","type":"uint256"}],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"}],"name":"getTotalCollateral","outputs":[{"internalType":"uint256","name":"amountUSDC","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"},{"internalType":"address","name":"user","type":"address"}],"name":"getUserTokens","outputs":[{"internalType":"uint256","name":"yes","type":"uint256"},{"internalType":"uint256","name":"no","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"marketCreationFeeUsdc","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"},{"internalType":"address","name":"","type":"address"}],"name":"noTokens","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"outcomes","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"},{"internalType":"address","name":"signerSlot0","type":"address"},{"internalType":"address","name":"signerSlot1","type":"address"},{"internalType":"uint256","name":"collateralUsdAbsScaledSlot0","type":"uint256"},{"internalType":"uint256","name":"collateralUsdAbsScaledSlot1","type":"uint256"},{"internalType":"uint256","name":"qtyScaledSlot0","type":"uint256"},{"internalType":"uint256","name":"qtyScaledSlot1","type":"uint256"},{"internalType":"uint128","name":"txIdSlot0","type":"uint128"},{"internalType":"uint128","name":"txIdSlot1","type":"uint128"},{"internalType":"bytes","name":"sigObjSlot0","type":"bytes"},{"internalType":"bytes","name":"sigObjSlot1","type":"bytes"},{"internalType":"bool","name":"primarySecondarySlot0","type":"bool"},{"internalType":"bool","name":"primarySecondarySlot1","type":"bool"}],"name":"posColToksOnBehalfAtomic","outputs":[{"internalType":"uint256","name":"yes","type":"uint256"},{"internalType":"uint256","name":"no","type":"uint256"},{"internalType":"uint256","name":"yes2","type":"uint256"},{"internalType":"uint256","name":"no2","type":"uint256"}],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"}],"name":"redeem","outputs":[{"internalType":"uint256","name":"amountUSDC","type":"uint256"}],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"},{"internalType":"address","name":"user_account","type":"address"}],"name":"redeemOnBehalfOfUser","outputs":[{"internalType":"uint256","name":"amountUSDC","type":"uint256"}],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"resolutionTimes","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"},{"internalType":"bool","name":"noYes","type":"bool"}],"name":"resolveMarket","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint256","name":"_marketCreationFeeUsdc","type":"uint256"}],"name":"setMarketCreationFee","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint256","name":"_rakePercentScaled100","type":"uint256"}],"name":"setRakeScaled100","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"statements","outputs":[{"internalType":"string","name":"","type":"string"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"totalCollateralUsd","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"usedTxIds","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"},{"internalType":"address","name":"","type":"address"}],"name":"yesTokens","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"}]

---

testnet:0.0.9070333

[{"inputs":[{"internalType":"address","name":"_collateralToken","type":"address"}],"stateMutability":"nonpayable","type":"constructor"},{"anonymous":false,"inputs":[{"indexed":false,"internalType":"uint128","name":"marketId","type":"uint128"},{"indexed":false,"internalType":"bool","name":"outcome","type":"bool"}],"name":"MarketResolved","type":"event"},{"anonymous":false,"inputs":[{"indexed":false,"internalType":"uint128","name":"marketId","type":"uint128"},{"indexed":true,"internalType":"address","name":"buyer","type":"address"},{"indexed":false,"internalType":"uint256","name":"collateralUsd","type":"uint256"},{"indexed":false,"internalType":"uint256","name":"qtyScaled","type":"uint256"},{"indexed":false,"internalType":"bool","name":"primarySecondary","type":"bool"}],"name":"PositionTokensPurchased","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"internalType":"address","name":"token","type":"address"}],"name":"TokenAssociated","type":"event"},{"anonymous":false,"inputs":[{"indexed":false,"internalType":"uint128","name":"marketId","type":"uint128"},{"indexed":true,"internalType":"address","name":"winner","type":"address"},{"indexed":false,"internalType":"uint256","name":"amount","type":"uint256"}],"name":"WinningsRedeemed","type":"event"},{"inputs":[{"internalType":"address","name":"tokenAddress","type":"address"}],"name":"associateToken","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address","name":"","type":"address"}],"name":"associatedTokens","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"collateralToken","outputs":[{"internalType":"contract IERC20","name":"","type":"address"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"collateralTokenNdecimals","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"},{"internalType":"string","name":"_statement","type":"string"}],"name":"createNewMarket","outputs":[{"internalType":"uint256","name":"allowance","type":"uint256"}],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"}],"name":"getTotalCollateral","outputs":[{"internalType":"uint256","name":"amountUSDC","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"},{"internalType":"address","name":"user","type":"address"}],"name":"getUserTokens","outputs":[{"internalType":"uint256","name":"yes","type":"uint256"},{"internalType":"uint256","name":"no","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"marketCreationFeeUsdc","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"},{"internalType":"address","name":"","type":"address"}],"name":"noTokens","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"outcomes","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"},{"internalType":"address","name":"signerYes","type":"address"},{"internalType":"address","name":"signerNo","type":"address"},{"internalType":"uint256","name":"collateralUsdAbsScaledYes","type":"uint256"},{"internalType":"uint256","name":"collateralUsdAbsScaledNo","type":"uint256"},{"internalType":"uint256","name":"qtyScaledYes","type":"uint256"},{"internalType":"uint256","name":"qtyScaledNo","type":"uint256"},{"internalType":"uint128","name":"txIdYes","type":"uint128"},{"internalType":"uint128","name":"txIdNo","type":"uint128"},{"internalType":"bytes","name":"sigObjYes","type":"bytes"},{"internalType":"bytes","name":"sigObjNo","type":"bytes"},{"internalType":"bool","name":"primarySecondaryYes","type":"bool"},{"internalType":"bool","name":"primarySecondaryNo","type":"bool"}],"name":"posColToksOnBehalfAtomic","outputs":[{"internalType":"uint256","name":"yes","type":"uint256"},{"internalType":"uint256","name":"no","type":"uint256"},{"internalType":"uint256","name":"yes2","type":"uint256"},{"internalType":"uint256","name":"no2","type":"uint256"}],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"}],"name":"redeem","outputs":[{"internalType":"uint256","name":"amountUSDC","type":"uint256"}],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"resolutionTimes","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"},{"internalType":"bool","name":"noYes","type":"bool"}],"name":"resolveMarket","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint256","name":"_marketCreationFeeUsdc","type":"uint256"}],"name":"setMarketCreationFee","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint256","name":"_rakePercentScaled100","type":"uint256"}],"name":"setRakeScaled100","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"statements","outputs":[{"internalType":"string","name":"","type":"string"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"totalCollateralUsd","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"usedTxIds","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"},{"internalType":"address","name":"","type":"address"}],"name":"yesTokens","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"}]

---

testnet:0.0.8947052

[{"inputs":[{"internalType":"address","name":"_collateralToken","type":"address"}],"stateMutability":"nonpayable","type":"constructor"},{"anonymous":false,"inputs":[{"indexed":false,"internalType":"uint128","name":"marketId","type":"uint128"},{"indexed":false,"internalType":"bool","name":"outcome","type":"bool"}],"name":"MarketResolved","type":"event"},{"anonymous":false,"inputs":[{"indexed":false,"internalType":"uint128","name":"marketId","type":"uint128"},{"indexed":true,"internalType":"address","name":"buyer","type":"address"},{"indexed":false,"internalType":"uint256","name":"collateralUsd","type":"uint256"},{"indexed":false,"internalType":"uint256","name":"qtyScaled","type":"uint256"},{"indexed":false,"internalType":"bool","name":"primarySecondary","type":"bool"}],"name":"PositionTokensPurchased","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"internalType":"address","name":"token","type":"address"}],"name":"TokenAssociated","type":"event"},{"anonymous":false,"inputs":[{"indexed":false,"internalType":"uint128","name":"marketId","type":"uint128"},{"indexed":true,"internalType":"address","name":"winner","type":"address"},{"indexed":false,"internalType":"uint256","name":"amount","type":"uint256"}],"name":"WinningsRedeemed","type":"event"},{"inputs":[{"internalType":"address","name":"tokenAddress","type":"address"}],"name":"associateToken","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address","name":"","type":"address"}],"name":"associatedTokens","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"collateralToken","outputs":[{"internalType":"contract IERC20","name":"","type":"address"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"collateralTokenNdecimals","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"},{"internalType":"string","name":"_statement","type":"string"}],"name":"createNewMarket","outputs":[{"internalType":"uint256","name":"allowance","type":"uint256"}],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"}],"name":"getTotalCollateral","outputs":[{"internalType":"uint256","name":"amountUSDC","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"},{"internalType":"address","name":"user","type":"address"}],"name":"getUserTokens","outputs":[{"internalType":"uint256","name":"yes","type":"uint256"},{"internalType":"uint256","name":"no","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"marketCreationFeeUsdc","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"},{"internalType":"address","name":"","type":"address"}],"name":"noTokens","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"outcomes","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"},{"internalType":"address","name":"signerYes","type":"address"},{"internalType":"address","name":"signerNo","type":"address"},{"internalType":"uint256","name":"collateralUsdAbsScaledYes","type":"uint256"},{"internalType":"uint256","name":"collateralUsdAbsScaledNo","type":"uint256"},{"internalType":"uint256","name":"qtyScaledYes","type":"uint256"},{"internalType":"uint256","name":"qtyScaledNo","type":"uint256"},{"internalType":"uint128","name":"txIdYes","type":"uint128"},{"internalType":"uint128","name":"txIdNo","type":"uint128"},{"internalType":"bytes","name":"sigObjYes","type":"bytes"},{"internalType":"bytes","name":"sigObjNo","type":"bytes"},{"internalType":"bool","name":"primarySecondaryYes","type":"bool"},{"internalType":"bool","name":"primarySecondaryNo","type":"bool"}],"name":"posColToksOnBehalfAtomic","outputs":[{"internalType":"uint256","name":"yes","type":"uint256"},{"internalType":"uint256","name":"no","type":"uint256"},{"internalType":"uint256","name":"yes2","type":"uint256"},{"internalType":"uint256","name":"no2","type":"uint256"}],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"}],"name":"redeem","outputs":[{"internalType":"uint256","name":"amountUSDC","type":"uint256"}],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"resolutionTimes","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"},{"internalType":"bool","name":"noYes","type":"bool"}],"name":"resolveMarket","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint256","name":"_marketCreationFeeUsdc","type":"uint256"}],"name":"setMarketCreationFee","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"statements","outputs":[{"internalType":"string","name":"","type":"string"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"totalCollateralUsd","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"usedTxIds","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"},{"internalType":"address","name":"","type":"address"}],"name":"yesTokens","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"}]

---

testnet:0.0.8946970

[{"inputs":[{"internalType":"address","name":"_collateralToken","type":"address"}],"stateMutability":"nonpayable","type":"constructor"},{"anonymous":false,"inputs":[{"indexed":false,"internalType":"uint128","name":"marketId","type":"uint128"},{"indexed":false,"internalType":"bool","name":"outcome","type":"bool"}],"name":"MarketResolved","type":"event"},{"anonymous":false,"inputs":[{"indexed":false,"internalType":"uint128","name":"marketId","type":"uint128"},{"indexed":true,"internalType":"address","name":"buyer","type":"address"},{"indexed":false,"internalType":"uint256","name":"collateralUsd","type":"uint256"},{"indexed":false,"internalType":"uint256","name":"qtyScaled","type":"uint256"},{"indexed":false,"internalType":"bool","name":"primarySecondary","type":"bool"}],"name":"PositionTokensPurchased","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"internalType":"address","name":"token","type":"address"}],"name":"TokenAssociated","type":"event"},{"anonymous":false,"inputs":[{"indexed":false,"internalType":"uint128","name":"marketId","type":"uint128"},{"indexed":true,"internalType":"address","name":"winner","type":"address"},{"indexed":false,"internalType":"uint256","name":"amount","type":"uint256"}],"name":"WinningsRedeemed","type":"event"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"},{"internalType":"address","name":"from","type":"address"},{"internalType":"address","name":"to","type":"address"},{"internalType":"uint256","name":"yesAmount","type":"uint256"},{"internalType":"uint256","name":"noAmount","type":"uint256"}],"name":"adminTransferPositionTokens","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address","name":"tokenAddress","type":"address"}],"name":"associateToken","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address","name":"","type":"address"}],"name":"associatedTokens","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"collateralToken","outputs":[{"internalType":"contract IERC20","name":"","type":"address"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"collateralTokenNdecimals","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"},{"internalType":"string","name":"_statement","type":"string"}],"name":"createNewMarket","outputs":[{"internalType":"uint256","name":"allowance","type":"uint256"}],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"}],"name":"getTotalCollateral","outputs":[{"internalType":"uint256","name":"amountUSDC","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"},{"internalType":"address","name":"user","type":"address"}],"name":"getUserTokens","outputs":[{"internalType":"uint256","name":"yes","type":"uint256"},{"internalType":"uint256","name":"no","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"marketCreationFeeUsdc","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"},{"internalType":"address","name":"","type":"address"}],"name":"noTokens","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"outcomes","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"},{"internalType":"address","name":"signerYes","type":"address"},{"internalType":"address","name":"signerNo","type":"address"},{"internalType":"uint256","name":"collateralUsdAbsScaledYes","type":"uint256"},{"internalType":"uint256","name":"collateralUsdAbsScaledNo","type":"uint256"},{"internalType":"uint256","name":"qtyScaledYes","type":"uint256"},{"internalType":"uint256","name":"qtyScaledNo","type":"uint256"},{"internalType":"uint128","name":"txIdYes","type":"uint128"},{"internalType":"uint128","name":"txIdNo","type":"uint128"},{"internalType":"bytes","name":"sigObjYes","type":"bytes"},{"internalType":"bytes","name":"sigObjNo","type":"bytes"},{"internalType":"bool","name":"primarySecondaryYes","type":"bool"},{"internalType":"bool","name":"primarySecondaryNo","type":"bool"}],"name":"posColToksOnBehalfAtomic","outputs":[{"internalType":"uint256","name":"yes","type":"uint256"},{"internalType":"uint256","name":"no","type":"uint256"},{"internalType":"uint256","name":"yes2","type":"uint256"},{"internalType":"uint256","name":"no2","type":"uint256"}],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"}],"name":"redeem","outputs":[{"internalType":"uint256","name":"amountUSDC","type":"uint256"}],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"resolutionTimes","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"},{"internalType":"bool","name":"noYes","type":"bool"}],"name":"resolveMarket","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint256","name":"_marketCreationFeeUsdc","type":"uint256"}],"name":"setMarketCreationFee","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"statements","outputs":[{"internalType":"string","name":"","type":"string"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"totalCollateralUsd","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"usedTxIds","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"},{"internalType":"address","name":"","type":"address"}],"name":"yesTokens","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"}]

```
