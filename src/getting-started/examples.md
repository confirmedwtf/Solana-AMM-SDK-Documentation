# Examples

Here are some examples of how to use the Solana AMM SDK. Ready to copy and paste!

## Example 1: Generate only makers

```javascript
import { Connection, Keypair, PublicKey } from "@solana/web3.js"
import { Amm } from "@confirmedwtf/solana-amm-sdk"

// Replace with your RPC URL from QuickNode/Shyft/etc
const connection = new Connection("https://your-endpoint.network.quiknode.pro/abc123...")
// If you need a RPC URL, you can contact us on https://discord.gg/confirmedwtf for a free one

// Replace with your token's mint address
const mint = new PublicKey("YOUR_TOKEN_MINT")

// Add your wallet's private key (choose one method):
// Method 1: Using Phantom/wallet private key
const payerWallet = Keypair.fromSecretKey(bs58.decode("4wBqpZM9...your-private-key..."))

// Method 2: Using array format
// const payerWallet = Keypair.fromSecretKey(Uint8Array.from([123,456...]))

// Optional: Disable console logs
const amm = new Amm(connection, payerWallet, { disableLogs: true })

// Create makers only - using Raydium DEX specifically
await amm.makers(mint, 5000, {
    includeDexes: ["Raydium"], 
    jitoTipLamports: 100000
}) 
```

## Example 2: Generate volume only

```javascript
import { Connection, Keypair, PublicKey } from "@solana/web3.js"
import { Amm } from "@confirmedwtf/solana-amm-sdk"

const connection = new Connection("https://your-endpoint.network.quiknode.pro/abc123...")
const mint = new PublicKey("YOUR_TOKEN_MINT")
const payerWallet = Keypair.fromSecretKey(bs58.decode("4wBqpZM9...your-private-key..."))

// Initialize AMM with logs disabled (optional)
const amm = new Amm(connection, payerWallet, { disableLogs: true })

// Generate volume only
const minSolPerSwap = 0.001 // sol per swap
const maxSolPerSwap = 0.002 // sol per swap
const mCapFactor = 1    // higher = price increases
const speedFactor = 1   // controls trading frequency

// Generate volume using only Raydium DEX
await amm.volume(
    mint, 
    minSolPerSwap, 
    maxSolPerSwap, 
    mCapFactor, 
    speedFactor, 
    {
        includeDexes: ["Raydium"],
        jitoTipLamports: 100000
    }
)
```

## Example 3: Single Swap

```javascript
import { Connection, Keypair, PublicKey } from "@solana/web3.js"
import { Amm } from "@confirmedwtf/solana-amm-sdk"

const connection = new Connection("https://your-endpoint.network.quiknode.pro/abc123...")
const mint = new PublicKey("YOUR_TOKEN_MINT")
const payerWallet = Keypair.fromSecretKey(bs58.decode("4wBqpZM9...your-private-key..."))

const amm = new Amm(connection, payerWallet)

// Perform a single buy swap for 0.001 SOL
const swap = await amm.swap(
    mint, 
    "buy", 
    0.001, 
    {
        jitoTipLamports: 100000
    }
)
```

## Example 4: Combined Makers and Volume

```javascript
import { Connection, Keypair, PublicKey } from "@solana/web3.js"
import { Amm } from "@confirmedwtf/solana-amm-sdk"

const connection = new Connection("https://your-endpoint.network.quiknode.pro/abc123...")
const mint = new PublicKey("YOUR_TOKEN_MINT")
const payerWallet = Keypair.fromSecretKey(bs58.decode("4wBqpZM9...your-private-key..."))

const amm = new Amm(connection, payerWallet, { disableLogs: true })

// Configuration for volume
const minSolPerSwap = 0.001
const maxSolPerSwap = 0.002
const mCapFactor = 1
const speedFactor = 1

// Create makers and generate volume in parallel using Raydium
await Promise.all([
    amm.makers(mint, 5000, { 
        includeDexes: ["Raydium"], 
        jitoTipLamports: 100000 
    }),
    amm.volume(
        mint, 
        minSolPerSwap, 
        maxSolPerSwap, 
        mCapFactor, 
        speedFactor, 
        { 
            includeDexes: ["Raydium"], 
            jitoTipLamports: 100000 
        }
    )
])
```

## Configuration Options

- `disableLogs`: Set to `true` to disable console logs
- `includeDexes`: Array of DEX names to use (e.g., `["Raydium"]`)
- `jitoTipLamports`: Transaction priority fee (recommended: 100000)
- `mCapFactor`: Controls price direction (0 = neutral, 1+ = increase)
- `speedFactor`: Controls trading frequency
- Supported DEXes: "Raydium", "Orca", "Meteora", "Pump.fun", "Moonshot"
