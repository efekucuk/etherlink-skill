# Etherlink vs Standard EVM Chains

Etherlink is EVM-compatible but has some unique characteristics.

## Key Characteristics

### 1. Native Currency
- **Etherlink**: XTZ (Tez)
- Same 18 decimals as ETH, different symbol and economics

### 2. Gas & Fees
- **EIP-1559 Supported**: Uses `max_fee_per_gas` field
- **No Priority Fees**: `max_priority_fee_per_gas` is ignored - sequencer uses first-come-first-served ordering
- **Fee Components**:
  - Execution fee: Varies with network throughput (minimum 1 gwei)
  - Inclusion fee: Covers data availability on Tezos L1
- Gas prices are typically very low

### 3. Block Hashes
Block hashes are computed differently on Etherlink. You cannot verify block hashes solely from the block header. This affects:
- Light client implementations
- Block hash verification tools

### 4. Finality
- ~500ms for sequencer confirmation
- ~8 seconds for data posted to Tezos L1
- Full finality after Tezos confirmation

### 5. WebSockets
- Supported when running your own node with `--ws` flag
- `eth_subscribe` works for newBlockHeaders, logs, etc.
- Public RPC nodes don't expose WebSocket endpoints publicly

## Supported RPC Methods

### Fully Supported ✅
- `eth_blockNumber`
- `eth_chainId`
- `eth_getBalance`
- `eth_getBlockByHash`
- `eth_getBlockByNumber`
- `eth_getTransactionByHash`
- `eth_getTransactionReceipt`
- `eth_call`
- `eth_estimateGas`
- `eth_gasPrice`
- `eth_maxPriorityFeePerGas`
- `eth_feeHistory`
- `eth_sendRawTransaction`
- `eth_getLogs`
- `eth_getCode`
- `eth_getStorageAt`
- `eth_getTransactionCount`
- `debug_traceTransaction`
- `debug_traceBlockByNumber`

### Requires Own Node ⚠️
- `eth_subscribe` (via WebSocket with `--ws` flag)

### Not Supported ❌
- `eth_syncing`
- `eth_newFilter`
- `eth_newBlockFilter`
- `eth_newPendingTransactionFilter`
- `eth_getFilterChanges`
- `eth_getFilterLogs`
- `eth_uninstallFilter`
- `engine_*` endpoints

## Bridging to Tezos L1

Etherlink connects to Tezos via a native bridge. This is NOT an EVM operation.

### Deposits (Tezos → Etherlink)
- Initiated on Tezos L1
- Requires Tezos wallet/tooling
- Takes ~10-15 minutes

### Withdrawals (Etherlink → Tezos)
- Initiated on Etherlink (EVM transaction)
- Finalized on Tezos after challenge period
- Takes ~2 weeks (optimistic rollup challenge period)

For bridge operations, use the official bridge UI or Tezos SDKs.

## Smart Contract Compatibility

Most Solidity/EVM contracts work unchanged. Watch for:
- Contracts relying on `PREVRANDAO` (may behave differently)
- Contracts verifying block hashes
- Contracts that depend on priority fee mechanics

## Best Practices

1. **Don't set priority fees** - they're ignored anyway
2. **Don't rely on block hashes** for verification
3. **Account for bridge delays** in UX
4. **Test on Shadownet first** - it mirrors mainnet behavior
5. **Run your own node** for WebSocket subscriptions
