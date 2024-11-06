# Fees

The Solana AMM SDK has a simple fee structure, but there are additional fees to consider when generating volume.

## Solana AMM SDK Fees
### Maker Fees
- **Bundle Fee**: 40,000 lamports per bundle (4 makers)
- **Transaction Cost**: 20,000 lamports per maker bundle

Example costs for different maker quantities:
- 1,000 makers: ~0.015 SOL
- 10,000 makers: ~0.15 SOL  
- 100,000 makers: ~1.5 SOL
- 1,000,000 makers: ~15 SOL

### Volume Fees
- **Volume Fee**: 0.05% of total volume generated + 12,500 lamports per tx. 

Example costs for different volume amounts:
- 10,000 SOL volume: 5 USD fee
- 100,000 SOL volume: 50 USD fee
- 1,000,000 SOL volume: 500 USD fee

## Additional Fees to Consider

When generating volume, you will also need to account for:

- **Liquidity Pool Fees**: These vary by provider
  - Raydium pools: 0.25% per swap
  - Meteora dynamic pools: Variable fees (can be higher than 0.25%)

Always check the specific fees for the liquidity pool you are using before generating volume, as these fees will impact your total costs.
