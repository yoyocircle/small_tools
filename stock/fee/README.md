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

The problem is broken down using a recursive dynamic programming strategy. Let \( dp[i] \) represent the minimum fee for trading `i` shares. The recurrence relation is:

$$ 
  dp[n] = \min (
    calculateFee(n),
    dp[n - nShares1Dollar] + 1,
    dp[n - nShares1Dollar * 2] + 2,
  )
$$


By solving smaller subproblems optimally and combining them, the algorithm efficiently computes the minimum fee for `n` shares.

### Greedy Optimization

For larger numbers of shares, a greedy strategy is employed alongside DP. Known configurations that yield minimal fees (like 1 NTD fee) are used as much as possible, reducing the problem size for DP processing.

### Output

- **Minimum Fee**: The optimal fee for trading `n` shares.
- **Transaction Breakdown**: The sequence of transactions (whole and odd lots) that yields the minimum fee.
