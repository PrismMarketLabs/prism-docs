# Prism Protocol Documentation

## Smart Contract ABI

```json
[{"inputs":[{"internalType":"address","name":"_collateralToken","type":"address"}],"stateMutability":"nonpayable","type":"constructor"},{"anonymous":false,"inputs":[{"indexed":false,"internalType":"int64","name":"responseCode","type":"int64"},{"indexed":false,"internalType":"address","name":"account","type":"address"},{"indexed":false,"internalType":"bool","name":"response","type":"bool"}],"name":"AccountAuthorizationResponse","type":"event"},{"anonymous":false,"inputs":[{"indexed":false,"internalType":"uint128","name":"marketId","type":"uint128"},{"indexed":false,"internalType":"bool","name":"outcome","type":"bool"}],"name":"MarketResolved","type":"event"},{"anonymous":false,"inputs":[{"indexed":false,"internalType":"uint128","name":"marketId","type":"uint128"},{"indexed":true,"internalType":"address","name":"buyer","type":"address"},{"indexed":false,"internalType":"uint256","name":"collateralUsd","type":"uint256"},{"indexed":false,"internalType":"uint256","name":"qtyScaled","type":"uint256"}],"name":"PositionTokensPurchased","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"internalType":"address","name":"token","type":"address"}],"name":"TokenAssociated","type":"event"},{"anonymous":false,"inputs":[{"indexed":false,"internalType":"uint128","name":"marketId","type":"uint128"},{"indexed":true,"internalType":"address","name":"user","type":"address"},{"indexed":false,"internalType":"uint256","name":"amount","type":"uint256"}],"name":"WinningsRedeemed","type":"event"},{"inputs":[{"internalType":"address","name":"tokenAddress","type":"address"}],"name":"associateToken","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address","name":"","type":"address"}],"name":"associatedTokens","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"},{"internalType":"address","name":"signerYes","type":"address"},{"internalType":"address","name":"signerNo","type":"address"},{"internalType":"uint256","name":"collateralUsdAbsScaledYes","type":"uint256"},{"internalType":"uint256","name":"collateralUsdAbsScaledNo","type":"uint256"},{"internalType":"uint256","name":"qtyScaledYes","type":"uint256"},{"internalType":"uint256","name":"qtyScaledNo","type":"uint256"},{"internalType":"uint128","name":"txIdYes","type":"uint128"},{"internalType":"uint128","name":"txIdNo","type":"uint128"},{"internalType":"bytes","name":"sigObjYes","type":"bytes"},{"internalType":"bytes","name":"sigObjNo","type":"bytes"}],"name":"buyPositionTokensOnBehalfAtomic","outputs":[{"internalType":"uint256","name":"yes","type":"uint256"},{"internalType":"uint256","name":"no","type":"uint256"},{"internalType":"uint256","name":"yes2","type":"uint256"},{"internalType":"uint256","name":"no2","type":"uint256"}],"stateMutability":"nonpayable","type":"function"},{"inputs":[],"name":"collateralToken","outputs":[{"internalType":"contract IERC20","name":"","type":"address"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"collateralTokenNdecimals","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"},{"internalType":"string","name":"_statement","type":"string"}],"name":"createNewMarket","outputs":[{"internalType":"uint256","name":"allowance","type":"uint256"}],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"}],"name":"getTotalCollateral","outputs":[{"internalType":"uint256","name":"amountUSDC","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"},{"internalType":"address","name":"user","type":"address"}],"name":"getUserTokens","outputs":[{"internalType":"uint256","name":"yes","type":"uint256"},{"internalType":"uint256","name":"no","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"marketCreationFeeUsdc","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"},{"internalType":"address","name":"","type":"address"}],"name":"noTokens","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"outcomes","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"}],"name":"redeem","outputs":[{"internalType":"uint256","name":"amountUSDC","type":"uint256"}],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"resolutionTimes","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"marketId","type":"uint128"},{"internalType":"bool","name":"noYes","type":"bool"}],"name":"resolveMarket","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint256","name":"_marketCreationFeeUsdc","type":"uint256"}],"name":"setMarketCreationFee","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"statements","outputs":[{"internalType":"string","name":"","type":"string"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"totalCollateralUsd","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"}],"name":"usedTxIds","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint128","name":"","type":"uint128"},{"internalType":"address","name":"","type":"address"}],"name":"yesTokens","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"}]
```

## Table of Contents

- [api.proto](#api-proto)
    - [CancelOrderRequest](#api-CancelOrderRequest)
    - [Category](#api-Category)
    - [CategoryIdRequest](#api-CategoryIdRequest)
    - [CategoryRequest](#api-CategoryRequest)
    - [CategoryResponse](#api-CategoryResponse)
    - [ChallengeRequest](#api-ChallengeRequest)
    - [ClobOrder](#api-ClobOrder)
    - [Comment](#api-Comment)
    - [CommentIdRequest](#api-CommentIdRequest)
    - [CreateCommentRequest](#api-CreateCommentRequest)
    - [CreateCommentResponse](#api-CreateCommentResponse)
    - [CreateMarketRequest](#api-CreateMarketRequest)
    - [CreateMarketResponse](#api-CreateMarketResponse)
    - [CreateMarketv2Request](#api-CreateMarketv2Request)
    - [Empty](#api-Empty)
    - [GetCommentsRequest](#api-GetCommentsRequest)
    - [GetCommentsResponse](#api-GetCommentsResponse)
    - [LimitOffsetRequest](#api-LimitOffsetRequest)
    - [MacroMetadataResponse](#api-MacroMetadataResponse)
    - [MacroMetadataResponse.SmartContractIdsEntry](#api-MacroMetadataResponse-SmartContractIdsEntry)
    - [MacroMetadataResponse.TokenIdsEntry](#api-MacroMetadataResponse-TokenIdsEntry)
    - [MacroMetadataResponse.TotalVolumeUsdEntry](#api-MacroMetadataResponse-TotalVolumeUsdEntry)
    - [MacroMetadataResponse.UsdcTokenIdsEntry](#api-MacroMetadataResponse-UsdcTokenIdsEntry)
    - [MarketIdRequest](#api-MarketIdRequest)
    - [MarketResponse](#api-MarketResponse)
    - [MarketsResponse](#api-MarketsResponse)
    - [Match](#api-Match)
    - [MatchesResponse](#api-MatchesResponse)
    - [NewsLetterRequest](#api-NewsLetterRequest)
    - [Position](#api-Position)
    - [PositionInfo](#api-PositionInfo)
    - [PositionsResponse](#api-PositionsResponse)
    - [PredictionIntent](#api-PredictionIntent)
    - [PredictionIntents](#api-PredictionIntents)
    - [PredictionIntentsResponse](#api-PredictionIntentsResponse)
    - [PriceHistoryRequest](#api-PriceHistoryRequest)
    - [PriceHistoryResponse](#api-PriceHistoryResponse)
    - [PrismPredictionIntentRequest](#api-PrismPredictionIntentRequest)
    - [ResolveMarketRequest](#api-ResolveMarketRequest)
    - [StdResponse](#api-StdResponse)
    - [UpdateMarketRequest](#api-UpdateMarketRequest)
    - [UserPortfolioRequest](#api-UserPortfolioRequest)
    - [UserPortfolioResponse](#api-UserPortfolioResponse)
    - [UserPortfolioResponse.OpenPredictionIntentsEntry](#api-UserPortfolioResponse-OpenPredictionIntentsEntry)
    - [UserPortfolioResponse.PositionsEntry](#api-UserPortfolioResponse-PositionsEntry)
    - [VerifyChallengeRequest](#api-VerifyChallengeRequest)
  
    - [ApiAuth](#api-ApiAuth)
    - [ApiServicePublic](#api-ApiServicePublic)
  
- [Scalar Value Types](#scalar-value-types)



<a name="api-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## api.proto
Use lower_snake_case for field names (Google Protobuf Style Guide)
Use json_name option for precise JSON serde - use protojson to Marshal/Unmarshal


<a name="api-CancelOrderRequest"></a>

### CancelOrderRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| market_id | [string](#string) |  |  |
| tx_id | [string](#string) |  |  |






<a name="api-Category"></a>

### Category



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| id | [int32](#int32) |  |  |
| name | [string](#string) |  |  |






<a name="api-CategoryIdRequest"></a>

### CategoryIdRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| category_id | [int32](#int32) |  |  |






<a name="api-CategoryRequest"></a>

### CategoryRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| category_id | [int32](#int32) | optional |  |
| name | [string](#string) |  |  |
| is_active | [bool](#bool) |  |  |
| description | [string](#string) |  |  |






<a name="api-CategoryResponse"></a>

### CategoryResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| id | [int32](#int32) |  |  |
| name | [string](#string) |  |  |
| is_active | [bool](#bool) |  |  |
| description | [string](#string) |  |  |






<a name="api-ChallengeRequest"></a>

### ChallengeRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| account_id | [string](#string) |  |  |
| network | [string](#string) |  |  |






<a name="api-ClobOrder"></a>

### ClobOrder



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| market_id | [string](#string) |  |  |
| tx_id | [string](#string) |  |  |






<a name="api-Comment"></a>

### Comment



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| account_id | [string](#string) |  | string comment_id = 1 [json_name = &#34;commentId&#34;]; |
| content | [string](#string) |  |  |
| sig | [string](#string) |  |  |
| public_key | [string](#string) |  |  |
| key_type | [uint32](#uint32) |  |  |
| created_at | [string](#string) |  |  |






<a name="api-CommentIdRequest"></a>

### CommentIdRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| comment_id | [int32](#int32) |  |  |






<a name="api-CreateCommentRequest"></a>

### CreateCommentRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| market_id | [string](#string) |  |  |
| account_id | [string](#string) |  |  |
| content | [string](#string) |  |  |
| sig | [string](#string) |  |  |
| public_key | [string](#string) |  |  |
| key_type | [uint32](#uint32) |  |  |






<a name="api-CreateCommentResponse"></a>

### CreateCommentResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| comment | [Comment](#api-Comment) |  |  |






<a name="api-CreateMarketRequest"></a>

### CreateMarketRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| market_id | [string](#string) |  |  |
| net | [string](#string) |  |  |
| statement | [string](#string) |  |  |
| image_url | [string](#string) |  |  |
| closes_at | [string](#string) | optional | string smart_contract_id = 5; // not needed - smart_contract_id is added to the markets table at run-time based on the net |
| description | [string](#string) |  |  |






<a name="api-CreateMarketResponse"></a>

### CreateMarketResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| market_response | [MarketResponse](#api-MarketResponse) |  |  |
| remaining_allowance | [uint64](#uint64) |  |  |






<a name="api-CreateMarketv2Request"></a>

### CreateMarketv2Request



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| market_id | [string](#string) |  |  |
| net | [string](#string) |  |  |
| statement | [string](#string) |  |  |
| closes_at | [string](#string) | optional |  |
| description | [string](#string) |  |  |
| category_ids | [int32](#int32) | repeated | a market must have at least 1 category and at most 5 categories |
| img_chunk | [bytes](#bytes) |  | max 5 MB per chunk |
| img_file_name | [string](#string) |  | max 255 chars for file name |
| img_mime_type | [string](#string) |  | restrict to common image MIME types |






<a name="api-Empty"></a>

### Empty







<a name="api-GetCommentsRequest"></a>

### GetCommentsRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| market_id | [string](#string) |  |  |
| limit | [int32](#int32) | optional |  |
| offset | [int32](#int32) | optional |  |






<a name="api-GetCommentsResponse"></a>

### GetCommentsResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| comments | [Comment](#api-Comment) | repeated |  |






<a name="api-LimitOffsetRequest"></a>

### LimitOffsetRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| limit | [int32](#int32) |  |  |
| offset | [int32](#int32) |  |  |






<a name="api-MacroMetadataResponse"></a>

### MacroMetadataResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| available_networks | [string](#string) | repeated |  |
| available_networks_admin | [string](#string) | repeated |  |
| smart_contract_ids | [MacroMetadataResponse.SmartContractIdsEntry](#api-MacroMetadataResponse-SmartContractIdsEntry) | repeated |  |
| usdc_token_ids | [MacroMetadataResponse.UsdcTokenIdsEntry](#api-MacroMetadataResponse-UsdcTokenIdsEntry) | repeated |  |
| usdc_decimals | [uint32](#uint32) |  |  |
| market_creation_fee_scaled_usdc | [uint64](#uint64) |  |  |
| n_markets | [uint32](#uint32) |  |  |
| token_ids | [MacroMetadataResponse.TokenIdsEntry](#api-MacroMetadataResponse-TokenIdsEntry) | repeated |  |
| min_order_size_usd | [double](#double) |  |  |
| tv_pending_usd | [double](#double) |  |  |
| tv_matched_usd | [double](#double) |  |  |
| tvl_usd | [double](#double) |  |  |
| total_volume_usd | [MacroMetadataResponse.TotalVolumeUsdEntry](#api-MacroMetadataResponse-TotalVolumeUsdEntry) | repeated |  |
| active_traders | [uint32](#uint32) |  |  |
| categories | [Category](#api-Category) | repeated |  |






<a name="api-MacroMetadataResponse-SmartContractIdsEntry"></a>

### MacroMetadataResponse.SmartContractIdsEntry



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| key | [string](#string) |  |  |
| value | [string](#string) |  |  |






<a name="api-MacroMetadataResponse-TokenIdsEntry"></a>

### MacroMetadataResponse.TokenIdsEntry



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| key | [string](#string) |  |  |
| value | [string](#string) |  |  |






<a name="api-MacroMetadataResponse-TotalVolumeUsdEntry"></a>

### MacroMetadataResponse.TotalVolumeUsdEntry



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| key | [string](#string) |  |  |
| value | [double](#double) |  |  |






<a name="api-MacroMetadataResponse-UsdcTokenIdsEntry"></a>

### MacroMetadataResponse.UsdcTokenIdsEntry



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| key | [string](#string) |  |  |
| value | [string](#string) |  |  |






<a name="api-MarketIdRequest"></a>

### MarketIdRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| market_id | [string](#string) |  |  |






<a name="api-MarketResponse"></a>

### MarketResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| market_id | [string](#string) |  |  |
| net | [string](#string) |  |  |
| statement | [string](#string) |  |  |
| is_paused | [bool](#bool) |  |  |
| is_suspended | [bool](#bool) |  |  |
| created_at | [string](#string) |  |  |
| resolved_at | [string](#string) |  |  |
| image_url | [string](#string) |  |  |
| price_usd | [float](#float) |  |  |
| description | [string](#string) |  | string smart_contract_id = 9 [json_name = &#34;smartContractId&#34;]; // not needed - smart_contract_id is a column in the markets table |
| closes_at | [string](#string) |  |  |
| outcome | [bool](#bool) | optional |  |
| smart_contract_id | [string](#string) |  |  |
| category_ids | [int32](#int32) | repeated |  |






<a name="api-MarketsResponse"></a>

### MarketsResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| markets | [MarketResponse](#api-MarketResponse) | repeated |  |






<a name="api-Match"></a>

### Match



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| market_id | [string](#string) |  |  |
| tx_id1 | [string](#string) |  |  |
| tx_id2 | [string](#string) |  |  |
| price_usd | [double](#double) |  |  |
| qty1 | [double](#double) |  |  |
| qty2 | [double](#double) |  |  |
| created_at | [string](#string) |  |  |
| tx_hash | [string](#string) |  |  |






<a name="api-MatchesResponse"></a>

### MatchesResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| matches | [Match](#api-Match) | repeated |  |






<a name="api-NewsLetterRequest"></a>

### NewsLetterRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| email | [string](#string) |  |  |






<a name="api-Position"></a>

### Position



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| market_id | [string](#string) |  |  |
| evm_address | [string](#string) |  |  |
| yes | [uint64](#uint64) |  |  |
| no | [uint64](#uint64) |  |  |
| updated_at | [string](#string) |  |  |
| created_at | [string](#string) |  |  |






<a name="api-PositionInfo"></a>

### PositionInfo



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| position | [Position](#api-Position) |  |  |
| price_usd | [float](#float) |  |  |
| is_paused | [bool](#bool) |  |  |
| resolved_at | [string](#string) |  |  |






<a name="api-PositionsResponse"></a>

### PositionsResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| positions | [Position](#api-Position) | repeated |  |






<a name="api-PredictionIntent"></a>

### PredictionIntent



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| tx_id | [string](#string) |  |  |
| net | [string](#string) |  |  |
| market_id | [string](#string) |  |  |
| generated_at | [string](#string) |  |  |
| account_id | [string](#string) |  |  |
| market_limit | [string](#string) |  |  |
| price_usd | [double](#double) |  |  |
| qty | [double](#double) |  |  |






<a name="api-PredictionIntents"></a>

### PredictionIntents



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| prediction_intents | [PredictionIntent](#api-PredictionIntent) | repeated |  |






<a name="api-PredictionIntentsResponse"></a>

### PredictionIntentsResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| prediction_intents | [PrismPredictionIntentRequest](#api-PrismPredictionIntentRequest) | repeated |  |






<a name="api-PriceHistoryRequest"></a>

### PriceHistoryRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| market_id | [string](#string) |  |  |
| net | [string](#string) |  |  |
| resolution | [string](#string) |  |  |
| from | [string](#string) |  |  |
| to | [string](#string) |  |  |
| limit | [int32](#int32) | optional |  |
| offset | [int32](#int32) | optional |  |






<a name="api-PriceHistoryResponse"></a>

### PriceHistoryResponse
want [timestampMs[], priceUsd[]] for graphing (e.g. uplot)


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| timestamp_ms | [uint64](#uint64) | repeated |  |
| price_usd | [float](#float) | repeated |  |






<a name="api-PrismPredictionIntentRequest"></a>

### PrismPredictionIntentRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| tx_id | [string](#string) |  |  |
| net | [string](#string) |  |  |
| market_id | [string](#string) |  |  |
| generated_at | [string](#string) |  |  |
| account_id | [string](#string) |  |  |
| market_limit | [string](#string) |  |  |
| price_usd | [double](#double) |  |  |
| qty | [double](#double) |  |  |
| sig | [string](#string) |  |  |
| public_key | [string](#string) |  | passing extra key info - i) avoid lookups ii) handle situation where user has changed their key |
| evm_address | [string](#string) |  |  |
| key_type | [uint32](#uint32) |  | string smart_contract_id = 9 [json_name = &#34;smartContractId&#34;]; // not needed - smart_contract_id is a column in the markets table |






<a name="api-ResolveMarketRequest"></a>

### ResolveMarketRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| market_id | [string](#string) |  |  |
| outcome | [bool](#bool) |  |  |






<a name="api-StdResponse"></a>

### StdResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| message | [string](#string) |  |  |
| error_code | [int32](#int32) |  |  |






<a name="api-UpdateMarketRequest"></a>

### UpdateMarketRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| market_id | [string](#string) |  |  |
| category_ids | [int32](#int32) | repeated | a market must have at least 1 category and at most 5 categories |






<a name="api-UserPortfolioRequest"></a>

### UserPortfolioRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| evm_address | [string](#string) |  |  |
| net | [string](#string) |  |  |
| market_id | [string](#string) | optional |  |






<a name="api-UserPortfolioResponse"></a>

### UserPortfolioResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| positions | [UserPortfolioResponse.PositionsEntry](#api-UserPortfolioResponse-PositionsEntry) | repeated |  |
| open_prediction_intents | [UserPortfolioResponse.OpenPredictionIntentsEntry](#api-UserPortfolioResponse-OpenPredictionIntentsEntry) | repeated |  |






<a name="api-UserPortfolioResponse-OpenPredictionIntentsEntry"></a>

### UserPortfolioResponse.OpenPredictionIntentsEntry



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| key | [string](#string) |  |  |
| value | [PredictionIntents](#api-PredictionIntents) |  |  |






<a name="api-UserPortfolioResponse-PositionsEntry"></a>

### UserPortfolioResponse.PositionsEntry



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| key | [string](#string) |  |  |
| value | [PositionInfo](#api-PositionInfo) |  |  |






<a name="api-VerifyChallengeRequest"></a>

### VerifyChallengeRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| challenge_response_base64 | [string](#string) |  | base64 chars only, min 10 chars |
| payload | [string](#string) |  | string public_key = 2 [json_name = &#34;publicKey&#34;, (validate.rules).string = {pattern: &#34;^(04|03|02)[0-9a-fA-F]{32,256}$&#34;} /* uncompressed (04...) or compressed (02... or 03...) public key (ed25519, ecdsa, etc.) in hex format */]; uint32 key_type = 3 [json_name = &#34;keyType&#34;, (validate.rules).uint32 = {in: [1, 2]} /* 1 = ed25519, 2 = ecdsa_secp256k1 */];

min 5 chars, max 256 chars |
| challenge_request | [ChallengeRequest](#api-ChallengeRequest) |  | echo back the original challenge request for correlation |





 

 

 


<a name="api-ApiAuth"></a>

### ApiAuth


| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| GetChallenge | [ChallengeRequest](#api-ChallengeRequest) | [StdResponse](#api-StdResponse) |  |
| VerifyChallenge | [VerifyChallengeRequest](#api-VerifyChallengeRequest) | [StdResponse](#api-StdResponse) | pass the signature in the |




<a name="api-ApiServicePublic"></a>

### ApiServicePublic


| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| Health | [Empty](#api-Empty) | [StdResponse](#api-StdResponse) |  |
| NewsLetter | [NewsLetterRequest](#api-NewsLetterRequest) | [StdResponse](#api-StdResponse) |  |
| CreatePredictionIntent | [PrismPredictionIntentRequest](#api-PrismPredictionIntentRequest) | [StdResponse](#api-StdResponse) |  |
| GetMarketById | [MarketIdRequest](#api-MarketIdRequest) | [MarketResponse](#api-MarketResponse) |  |
| GetMarkets | [LimitOffsetRequest](#api-LimitOffsetRequest) | [MarketsResponse](#api-MarketsResponse) |  |
| PriceHistory | [PriceHistoryRequest](#api-PriceHistoryRequest) | [PriceHistoryResponse](#api-PriceHistoryResponse) |  |
| MacroMetadata | [Empty](#api-Empty) | [MacroMetadataResponse](#api-MacroMetadataResponse) | general market data - volume, nMarkets, TVL, liquidity, etc. |
| CreateComment | [CreateCommentRequest](#api-CreateCommentRequest) | [CreateCommentResponse](#api-CreateCommentResponse) |  |
| GetComments | [GetCommentsRequest](#api-GetCommentsRequest) | [GetCommentsResponse](#api-GetCommentsResponse) |  |
| GetUserPortfolio | [UserPortfolioRequest](#api-UserPortfolioRequest) | [UserPortfolioResponse](#api-UserPortfolioResponse) |  |
| CancelPredictionIntent | [CancelOrderRequest](#api-CancelOrderRequest) | [StdResponse](#api-StdResponse) |  |
| CreateMarket | [CreateMarketRequest](#api-CreateMarketRequest) | [CreateMarketResponse](#api-CreateMarketResponse) | authenticated endpoints |
| CreateMarketv2 | [CreateMarketv2Request](#api-CreateMarketv2Request) | [CreateMarketResponse](#api-CreateMarketResponse) |  |
| UpdateMarket | [UpdateMarketRequest](#api-UpdateMarketRequest) | [StdResponse](#api-StdResponse) |  |
| GetAllMatches | [LimitOffsetRequest](#api-LimitOffsetRequest) | [MatchesResponse](#api-MatchesResponse) |  |
| GetAllPositions | [LimitOffsetRequest](#api-LimitOffsetRequest) | [PositionsResponse](#api-PositionsResponse) |  |
| GetAllPredictionIntents | [LimitOffsetRequest](#api-LimitOffsetRequest) | [PredictionIntentsResponse](#api-PredictionIntentsResponse) |  |
| ToggleMarketPause | [MarketIdRequest](#api-MarketIdRequest) | [StdResponse](#api-StdResponse) |  |
| ToggleMarketSuspend | [MarketIdRequest](#api-MarketIdRequest) | [StdResponse](#api-StdResponse) |  |
| DeleteComment | [CommentIdRequest](#api-CommentIdRequest) | [StdResponse](#api-StdResponse) |  |
| ResolveMarket | [ResolveMarketRequest](#api-ResolveMarketRequest) | [StdResponse](#api-StdResponse) |  |
| CreateCategory | [CategoryRequest](#api-CategoryRequest) | [CategoryResponse](#api-CategoryResponse) |  |
| UpdateCategory | [CategoryRequest](#api-CategoryRequest) | [CategoryResponse](#api-CategoryResponse) |  |
| DeleteCategory | [CategoryIdRequest](#api-CategoryIdRequest) | [StdResponse](#api-StdResponse) |  |

 



## Scalar Value Types

| .proto Type | Notes | C++ | Java | Python | Go | C# | PHP | Ruby |
| ----------- | ----- | --- | ---- | ------ | -- | -- | --- | ---- |
| <a name="double" /> double |  | double | double | float | float64 | double | float | Float |
| <a name="float" /> float |  | float | float | float | float32 | float | float | Float |
| <a name="int32" /> int32 | Uses variable-length encoding. Inefficient for encoding negative numbers – if your field is likely to have negative values, use sint32 instead. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="int64" /> int64 | Uses variable-length encoding. Inefficient for encoding negative numbers – if your field is likely to have negative values, use sint64 instead. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="uint32" /> uint32 | Uses variable-length encoding. | uint32 | int | int/long | uint32 | uint | integer | Bignum or Fixnum (as required) |
| <a name="uint64" /> uint64 | Uses variable-length encoding. | uint64 | long | int/long | uint64 | ulong | integer/string | Bignum or Fixnum (as required) |
| <a name="sint32" /> sint32 | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int32s. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="sint64" /> sint64 | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int64s. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="fixed32" /> fixed32 | Always four bytes. More efficient than uint32 if values are often greater than 2^28. | uint32 | int | int | uint32 | uint | integer | Bignum or Fixnum (as required) |
| <a name="fixed64" /> fixed64 | Always eight bytes. More efficient than uint64 if values are often greater than 2^56. | uint64 | long | int/long | uint64 | ulong | integer/string | Bignum |
| <a name="sfixed32" /> sfixed32 | Always four bytes. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="sfixed64" /> sfixed64 | Always eight bytes. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="bool" /> bool |  | bool | boolean | boolean | bool | bool | boolean | TrueClass/FalseClass |
| <a name="string" /> string | A string must always contain UTF-8 encoded or 7-bit ASCII text. | string | String | str/unicode | string | string | string | String (UTF-8) |
| <a name="bytes" /> bytes | May contain any arbitrary sequence of bytes. | string | ByteString | str | []byte | ByteString | string | String (ASCII-8BIT) |

