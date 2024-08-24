# Stock Trading Fee Optimization Algorithm

This repository implements a dynamic programming (DP) algorithm to minimize stock trading transaction fees. The goal is to determine the optimal way to split `n` shares into transactions, balancing whole lots (multiples of 1000 shares) and odd lots (less than 1000 shares), each with different fee structures.

## Algorithm Overview

### Key Concepts

- **Whole Lot Fee**: For whole lot transactions (multiples of 1000 shares), the fee is:
  \[
  \text{Fee}_{\text{whole}} = \max(\text{price} \times k \times \text{FEE\_RATE} \times \text{discount}, \text{minFee}_{\text{whole}})
  \]

- **Odd Lot Fee**: For odd lot transactions (less than 1000 shares), the fee is:
  \[
  \text{Fee}_{\text{odd}} = \max(\text{price} \times k \times \text{FEE\_RATE} \times \text{discount}, \text{minFee}_{\text{odd}})
  \]

### Dynamic Programming Approach

The problem is broken down using a recursive dynamic programming strategy. Let \( dp[i] \) represent the minimum fee for trading `i` shares. The recurrence relation is:

\[
dp[n] = \min \left( \text{calculateFee}(n), \, dp[n - k_{\text{whole}}] + \text{Fee}_{\text{whole}}(k_{\text{whole}}), \, dp[n - k_{\text{odd}}] + \text{Fee}_{\text{odd}}(k_{\text{odd}}) \right)
\]

Where:
- \( k_{\text{whole}} \) is a multiple of 1000.
- \( k_{\text{odd}} \in [1, 999] \).

By solving smaller subproblems optimally and combining them, the algorithm efficiently computes the minimum fee for `n` shares.

### Greedy Optimization

For larger numbers of shares, a greedy strategy is employed alongside DP. Known configurations that yield minimal fees (like 1 NTD fee) are used as much as possible, reducing the problem size for DP processing.

### Output

- **Minimum Fee**: The optimal fee for trading `n` shares.
- **Transaction Breakdown**: The sequence of transactions (whole and odd lots) that yields the minimum fee.
