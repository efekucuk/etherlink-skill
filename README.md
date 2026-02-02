# Etherlink Skill

A [ClawdHub](https://clawdhub.com) skill for interacting with **Etherlink** - an EVM-compatible Layer 2 blockchain built on Tezos.

## What's Included

- `SKILL.md` - Agent instructions for Etherlink operations
- `references/networks.md` - Network configs, RPC endpoints, MetaMask setup
- `references/differences.md` - How Etherlink differs from standard EVM chains
- `references/mcp-setup.md` - MCP server configuration guide
- `scripts/test-connection.sh` - Quick RPC health check

## Networks

| Network | Chain ID | RPC | Explorer |
|---------|----------|-----|----------|
| Mainnet | 42793 | https://node.mainnet.etherlink.com | [explorer.etherlink.com](https://explorer.etherlink.com) |
| Shadownet Testnet | 127823 | https://node.shadownet.etherlink.com | [shadownet.explorer.etherlink.com](https://shadownet.explorer.etherlink.com) |

**Native Currency:** XTZ (18 decimals)

## Installation

### Via ClawdHub
```bash
clawdhub install etherlink
```

### Manual
Clone this repo into your skills directory.

## Usage

This skill works with the [etherlink-mcp-server](https://github.com/efekucuk/etherlink-mcp-server). Configure the MCP server, then use natural language:

- "Get balance for 0x... on etherlink"
- "Send 0.1 XTZ to 0x... on etherlink"
- "Call balanceOf on contract 0x... on etherlink"

## Testnet Faucet

Get free testnet XTZ: https://shadownet.faucet.etherlink.com

## Resources

- [Etherlink Documentation](https://docs.etherlink.com/)
- [Block Explorer](https://explorer.etherlink.com)
- [etherlink-mcp-server](https://github.com/efekucuk/etherlink-mcp-server)

## License

MIT
