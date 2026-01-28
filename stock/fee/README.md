# Stock Trading Fee Optimization Algorithm

This repository implements a dynamic programming (DP) algorithm to minimize stock trading transaction fees and trading times. The goal is to determine the optimal way to split `n` shares into transactions, balancing whole lots (multiples of 1000 shares) and odd lots (less than 1000 shares), each with different fee structures.

## Algorithm Overview

### Key Concepts

- The transaction fee is:


  $$ Fee = \max ( minFee, price \times shares \times {FEE\\_RATE} \times discount) $$

  
- Two type of trading type:
  - whole: Minimal unit is 1000 shares
  - odd: Minmal unit is 1 share, maxinum is 999 shares. 

### Dynamic Programming Approach

The problem is broken down using a recursive dynamic programming strategy. Let \( dp[i] \) represent the minimum fee and transaction breakdown for trading `i` shares.

**Base case:** For small share counts (where fee ≤ 2 NTD), we precompute the optimal single odd-lot transaction.

**Recurrence relation:**

$$
dp[n] = \min \begin{cases}
  \text{calculateFee}(n) & \text{(single transaction)} \\
  dp[n - k_1] + dp[k_1] & \text{(split off } k_1 \text{ shares)} \\
  dp[n - k_2] + dp[k_2] & \text{(split off } k_2 \text{ shares)}
\end{cases}
$$

Where:
- \( k_1 \) = maximum shares that yield exactly 1 NTD fee (calculated from price and discount)
- \( k_2 \) = maximum shares where fee ≤ 2 NTD

By solving smaller subproblems optimally and combining them, the algorithm efficiently computes the minimum fee for `n` shares.

### Greedy Optimization

For larger numbers of shares, a greedy strategy is employed alongside DP. When \( k_1 \) (max shares for 1 NTD fee) is valid (i.e., within the odd-lot range), we greedily use as many \( k_1 \)-share transactions as possible, reducing the problem size for DP processing.

This optimization is only applied when:
- The share count is large enough (\( n \geq 2 \times k_2 \))
- \( k_1 \) is within the precomputed dp range (\( k_1 \leq k_2 \))

### Output

- **Minimum Fee**: The optimal fee for trading `n` shares.
- **Transaction Breakdown**: The sequence of transactions (whole and odd lots) that yields the minimum fee.
