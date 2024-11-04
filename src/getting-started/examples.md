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
const mint = new PublicKey("Ab9NePvx5PxqzqsKQmNrKz5264qJXH5xbL3NL8E6tYF1")

// Add your wallet's private key (choose one method):
// Method 1: Using Phantom/wallet private key
const payerWallet = Keypair.fromSecretKey(bs58.decode("4wBqpZM9...your-private-key..."))

// Method 2: Using array format
// const payerWallet = Keypair.fromSecretKey(Uint8Array.from([123,456...]))

// Create makers only
const amm = new Amm(connection, payerWallet)
await amm.makers(mint, 5000, {jitoTipLamports: 10001}) 
// This will generate 5000 makers 
```

## Example 2: Generate volume only

```javascript
import { Connection, Keypair, PublicKey } from "@solana/web3.js"
import { Amm } from "@confirmedwtf/solana-amm-sdk"

// Replace with your RPC URL from QuickNode/Shyft/etc
const connection = new Connection("https://your-endpoint.network.quiknode.pro/abc123...")
// If you need a RPC URL, you can contact us on https://discord.gg/confirmedwtf for a free one

// Replace with your token's mint address
const mint = new PublicKey("Ab9NePvx5PxqzqsKQmNrKz5264qJXH5xbL3NL8E6tYF1")

// Add your wallet's private key (choose one method):
// Method 1: Using Phantom/wallet private key
const payerWallet = Keypair.fromSecretKey(bs58.decode("4wBqpZM9...your-private-key..."))

// Method 2: Using array format
// const payerWallet = Keypair.fromSecretKey(Uint8Array.from([123,456...]))

// Generate volume only
const amm = new Amm(connection, payerWallet)
const minSolPerSwap = 0.005
const maxSolPerSwap = 0.006
const mCapFactor = 0    
const speedFactor = 1   // once every 10 seconds
await amm.volume(mint, minSolPerSwap, maxSolPerSwap, mCapFactor, speedFactor, {jitoTipLamports: 10001})
```

## Example 3: Both Makers and Volume

```javascript
import { Connection, Keypair, PublicKey } from "@solana/web3.js"
import { Amm } from "@confirmedwtf/solana-amm-sdk"

// Replace with your RPC URL from QuickNode/Shyft/etc
const connection = new Connection("https://your-endpoint.network.quiknode.pro/abc123...")
// If you need a RPC URL, you can contact us on https://discord.gg/confirmedwtf for a free one

// Replace with your token's mint address
const mint = new PublicKey("Ab9NePvx5PxqzqsKQmNrKz5264qJXH5xbL3NL8E6tYF1")

// Add your wallet's private key (choose one method):
// Method 1: Using Phantom/wallet private key
const payerWallet = Keypair.fromSecretKey(bs58.decode("4wBqpZM9...your-private-key..."))

// Method 2: Using array format
// const payerWallet = Keypair.fromSecretKey(Uint8Array.from([123,456...]))

const amm = new Amm(connection, payerWallet)

// Configuration for volume
const minSolPerSwap = 0.005
const maxSolPerSwap = 0.006
const mCapFactor = 0
const speedFactor = 1 // once every 10 seconds

// Create makers and generate volume in parallel
await Promise.all([
    amm.makers(mint, 5000, { jitoTipLamports: 10001 }),
    amm.volume(mint, minSolPerSwap, maxSolPerSwap, mCapFactor, speedFactor, { jitoTipLamports: 10001 })
])
```

