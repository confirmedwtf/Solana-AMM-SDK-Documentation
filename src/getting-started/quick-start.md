# Quick Start

This guide will help you get started with the Solana AMM SDK.

## Prerequisites

1. **Update your package list:**
    ```bash
    sudo apt-get update
    ```

2. **Install Node.js and npm:**
    ```bash
    sudo apt-get install -y nodejs npm
    ```
    - Verify installation by running: `node --version` and `npm --version`

3. **Install Git:**
    ```bash
    sudo apt-get install -y git
    ```
    - Verify installation by running: `git --version`

## Setup
1. **Choose your installation method:**

    Option A - Install via npm (Recommended):
    ```bash
    # Create a new directory and initialize
    mkdir my-amm-project
    cd my-amm-project
    npm init -y

    # Install the SDK
    npm install @confirmedwtf/solana-amm-sdk
    ```

    Option B - Clone the repository:
    ```bash
    git clone https://github.com/confirmedwtf/solana-amm-sdk
    cd solana-amm-sdk
    npm install
    ```

2. **Create test file:**
    - If you installed via npm, create a new `test.mjs` file
    - If you cloned the repository, the test file is already included
    
    You can copy our example test file from:
    https://github.com/confirmedwtf/solana-amm-sdk/blob/main/test.mjs

3. **Get a Solana RPC URL:**
    - Sign up at one of these providers:
        - [QuickNode](https://quicknode.com)
        - [Shyft](https://shyft.to)
        - [Helius](https://helius.xyz)
    - Create a new Solana endpoint
    - Copy your RPC URL (it will look like: `https://your-endpoint.network.quiknode.pro/abc123...`)

4. **Edit `test.mjs` using `nano`**
    
    ```bash
    nano test.mjs
    ```
    
    Before editing, ensure you have the following ready:
    
    - **RPC URL**: Your Solana RPC endpoint URL
    - **Token Mint Address**: The address of your token's mint on Solana
    - **Private Key**: Your wallet's private key (keep it secure)
    
    Update the necessary settings in the `test.mjs` file with your RPC URL, Token Mint address, and private key.

    To save and exit `nano`, follow these steps:
    - Press `Ctrl + X` to begin the exit process.
    - Press `Y` to confirm that you want to save the changes.
    - Press `Enter` to write the changes to the file and exit `nano`.

5. **Run the app:**
    ```bash
    node test.mjs
    ```
    - This command will start the application using the settings you configured in `test.mjs`.

6. **Stop the app:**
    - To stop the application, press `Ctrl + C` in the terminal where the app is running.

## Configuration Tips

- **RPC URL**: Use a reliable provider to avoid connection issues
- **Token Mint**: This is your token's address on Solana (can be found on Solscan/Explorer)
- **Makers Count**: 
    - Start with a smaller number (e.g., 1000) to test
    - Increase up to 5000+ for more market activity
- **Volume Settings**:
    - `mCapFactor`: 0 = neutral, 1 = moderate increase, 2+ = stronger increase
        - `mCapFactor` of 0 is neutral, meaning the price will not change
        - `mCapFactor` of 1 is price positive, meaning you will not sell all of the tokens you are buying while generating volume
    - `speedFactor`: This controls the delay between swaps. The average delay in seconds is calculated as `(5000 + 10000/2) / 1000 / speedFactor`. For example:
        - `speedFactor` of 1 results in an average delay of 10 seconds between swaps
        - `speedFactor` of 10 results in an average delay of 1 second between swaps
        - For a swap every minute, set `speedFactor` to approximately 0.167
        - For a swap every 5 minutes, set `speedFactor` to approximately 0.033
        - For a swap every 10 minutes, set `speedFactor` to approximately 0.017
    - `minSolPerSwap` and `maxSolPerSwap`: Start small (0.005-0.006) and adjust based on your needs
- **Jito Tip**: Set to 10001 to prioritize your transaction
- **Private Key**: Support for both base 58 string format and byte array format

## Important Notes

- Ensure you have enough SOL in your wallet (at least 0.03 SOL recommended)
- If transactions are not landing, try increasing the jito tip (defaults to 10000 lamports if not specified)
- Never share or commit your private keys
- Monitor your RPC usage to stay within provider limits

