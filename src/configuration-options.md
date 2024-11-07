# Configuration Options

This document details all available configuration options for the Confirmed.wtf Solana AMM SDK.

## Core Options

### AMM Initialization
```javascript
const amm = new Amm(connection, payerWallet, {
    disableLogs: true  // Optional: disable console logging
})
```

### Transaction Options
- `jitoTipLamports`: Transaction priority fee (default: 10000)
  - Recommended: 100000 for higher priority
  - Increase if transactions are not landing

## DEX Selection

### Supported DEXes
You can specify which DEXes to use via the `includeDexes` option. Supported values:

```javascript
const supportedDexes = [
    "Cropper",
    "Raydium",
    "Openbook",
    "StabbleWeightedSwap",
    "Guacswap",
    "OpenBookV2",
    "Aldrin",
    "MeteoraDLMM",
    "Saber(Decimals)",
    "SanctumInfinity",
    "Whirlpool",
    "StepN",
    "Dexlab",
    "RaydiumCP",
    "Mercurial",
    "LifinityV2",
    "ObricV2",
    "Meteora",
    "Phoenix",
    "TokenSwap",
    "HeliumNetwork",
    "Sanctum",
    "Moonshot",
    "StabbleStableSwap",
    "GooseFX",
    "Penguin",
    "AldrinV2",
    "OrcaV2",
    "LifinityV1",
    "1DEX",
    "CropperLegacy",
    "SolFi",
    "Oasis",
    "Saber",
    "Crema",
    "Pump.fun",
    "RaydiumCLMM",
    "Bonkswap",
    "Perps",
    "Fox",
    "Saros",
    "OrcaV1",
    "FluxBeam",
    "Invariant"
]
```

Usage example:
```javascript
await amm.volume(mint, minSolPerSwap, maxSolPerSwap, mCapFactor, speedFactor, {
    includeDexes: ["Raydium", "Orca", "Meteora"],
    jitoTipLamports: 100000
})
```

## Volume Generation Options

### mCapFactor
Controls price direction:
- `0`: Neutral (no price change)
- `1`: Moderate increase
- `2+`: Stronger increase

### speedFactor
Controls trading frequency. The average delay between swaps is calculated as:
```
(5000 + 10000/2) / 1000 / speedFactor seconds
```

Common settings:
- `1`: ~10 seconds between swaps
- `10`: ~1 second between swaps
- `0.167`: ~1 minute between swaps
- `0.033`: ~5 minutes between swaps
- `0.017`: ~10 minutes between swaps

### Swap Amounts
- `minSolPerSwap`: Minimum SOL per swap 
- `maxSolPerSwap`: Maximum SOL per swap 

## Maker Generation Options

### Number of Makers
```javascript
await amm.makers(mint, 5000, {  // 5000 makers
    includeDexes: ["Raydium"],
    jitoTipLamports: 100000
})
```

Recommended ranges:
- Testing: 1,000 makers
- Production: 5,000+ makers

## Private Key Formats

The SDK supports two private key formats:

1. Base58 String (e.g., from Phantom):
```javascript
const payerWallet = Keypair.fromSecretKey(bs58.decode("your-base58-private-key"))
```

2. Byte Array:
```javascript
const payerWallet = Keypair.fromSecretKey(Uint8Array.from([1,2,3...]))
```