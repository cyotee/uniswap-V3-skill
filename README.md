# Uniswap V3 Progressive Disclosure Skills

Progressive disclosure skills for developing with Uniswap V3, the concentrated liquidity AMM protocol. These skills cover core pool mechanics, tick-based pricing, position management, swap routing, and oracle integration.

## Installation

### Claude Code

Add as a submodule to your plugins directory:

```bash
git submodule add https://github.com/cyotee/uniswap-V3-skill.git plugins/uniswap-v3
```

Or clone directly:

```bash
git clone https://github.com/cyotee/uniswap-V3-skill.git
```

### OpenCode

Copy the `.opencode/skills/` directory contents to your local OpenCode skills directory.

## Skills

| Skill | Trigger Keywords | Description |
|-------|-----------------|-------------|
| `uniswap-v3-architecture` | protocol overview, V3 vs V2, concentrated liquidity intro | High-level architecture and design philosophy |
| `uniswap-v3-pool` | pool, UniswapV3Pool, slot0, liquidity state | Core pool contract mechanics and state |
| `uniswap-v3-ticks` | tick, tick spacing, tick math, bitmap | Tick system, price levels, and bitmap optimization |
| `uniswap-v3-positions` | position, fee growth, mint, burn, collect | Position tracking and fee accumulation |
| `uniswap-v3-swaps` | swap, exactInput, exactOutput, SwapRouter | Swap execution and multi-hop routing |
| `uniswap-v3-position-manager` | NonfungiblePositionManager, NFT, ERC721 | NFT-wrapped position management |
| `uniswap-v3-oracle` | oracle, TWAP, observations, observe | Time-weighted average price oracle system |
| `uniswap-v3-factory` | factory, createPool, fee tiers | Pool deployment and configuration |

## Key Concepts

### Concentrated Liquidity
Unlike V2's full-range liquidity, V3 allows LPs to concentrate their capital within specific price ranges (tick ranges). This dramatically improves capital efficiency—LPs can provide the same depth with less capital.

### Ticks and Tick Spacing
Prices are discretized into "ticks" where each tick represents a 0.01% (1.0001x) price change. Tick spacing determines which ticks can be initialized (e.g., 60 for 0.3% fee pools).

### Positions as NFTs
V3 positions are represented as ERC721 NFTs via NonfungiblePositionManager, enabling transferability and composability with other DeFi protocols.

### Fee Tiers
V3 supports multiple fee tiers per token pair:
- 0.01% (1 bps) - Stablecoin pairs
- 0.05% (5 bps) - Stable pairs
- 0.30% (30 bps) - Standard pairs
- 1.00% (100 bps) - Volatile pairs

### TWAP Oracle
Pools maintain cumulative tick observations enabling on-chain TWAP (time-weighted average price) calculations without external oracles.

## Repository Structure

### v3-core
```
contracts/
├── UniswapV3Pool.sol              # Core AMM pool
├── UniswapV3Factory.sol           # Pool factory
├── UniswapV3PoolDeployer.sol      # Deployment helper
├── interfaces/                     # Pool interfaces
└── libraries/
    ├── Tick.sol                   # Tick state management
    ├── TickBitmap.sol             # Packed tick lookup
    ├── Position.sol               # Position tracking
    ├── Oracle.sol                 # TWAP observations
    ├── TickMath.sol               # Tick↔Price conversion
    ├── SqrtPriceMath.sol          # Price delta math
    └── SwapMath.sol               # Swap step computation
```

### v3-periphery
```
contracts/
├── NonfungiblePositionManager.sol # ERC721 position wrapper
├── SwapRouter.sol                 # Swap execution
├── V3Migrator.sol                 # V2→V3 migration
├── base/                          # Composable base contracts
├── lens/
│   ├── Quoter.sol                 # Off-chain price quotes
│   └── TickLens.sol               # Tick enumeration
└── libraries/
    ├── LiquidityAmounts.sol       # Amount↔Liquidity conversion
    ├── PoolAddress.sol            # Deterministic pool addresses
    └── Path.sol                   # Multi-hop path encoding
```

## Deployed Addresses

### Ethereum Mainnet
- UniswapV3Factory: `0x1F98431c8aD98523631AE4a59f267346ea31F984`
- SwapRouter: `0xE592427A0AEce92De3Edee1F18E0157C05861564`
- NonfungiblePositionManager: `0xC36442b4a4522E871399CD717aBDD847Ab11FE88`
- Quoter: `0xb27308f9F90D607463bb33eA1BeBb41C27CE5AB6`

### Base, Arbitrum, Optimism, Polygon
See [Uniswap V3 Deployments](https://docs.uniswap.org/contracts/v3/reference/deployments)

## License

GPL-2.0-or-later
