# leet-day15

# Soup Servings Probability

## Problem Description

You are given two types of soup: type A and type B. Initially, you have `n` ml of each type of soup. There are four kinds of operations:

1. Serve 100 ml of soup A and 0 ml of soup B.
2. Serve 75 ml of soup A and 25 ml of soup B.
3. Serve 50 ml of soup A and 50 ml of soup B.
4. Serve 25 ml of soup A and 75 ml of soup B.

When you serve some soup, you give it to someone, and you no longer have it. Each turn, you will choose from the four operations with an equal probability of 0.25. If the remaining volume of soup is not enough to complete the operation, you will serve as much as possible. You stop once you no longer have some quantity of both types of soup.

Note that there is no operation where all 100 ml's of soup B are used first.

Return the probability that soup A will be empty first, plus half the probability that A and B become empty at the same time. Answers within 10^-5 of the actual answer will be accepted.

## Solution Approach

The probability of soup A becoming empty first or soup A and B becoming empty at the same time can be calculated using a recursive approach with memoization.

1. We define a recursive function `help(a, b, dp)` that takes the remaining ml of soup A `a`, the remaining ml of soup B `b`, and the memoization table `dp`.

2. In the `help` function, we check the base cases:
   - If both remaining ml of soup A and soup B are non-positive (`a <= 0` and `b <= 0`), we return `0.5`.
   - If the remaining ml of soup A is non-positive (`a <= 0`), we return `1.0`.
   - If the remaining ml of soup B is non-positive (`b <= 0`), we return `0.0`.

3. We define a vector `x` to store the four types of operations, each represented as a pair of integers. For each operation, we calculate the probability of choosing it as `0.25` and multiply it with the recursive call to `help` for the remaining ml of soup A and soup B after performing that operation.

4. We return the sum of probabilities calculated for all four operations as the result.

5. In the `soupServings` function, we handle a special case where `n` is greater than `5000`. In this case, we directly return `1.0` since the probability will be very close to 1.

6. Otherwise, we create a memoization table `dp` with dimensions `(n + 1) x (n + 1)` and initialize it with `-1`. We then call the `help` function with the initial remaining ml of soup A and soup B as `n` and return the result.

## Complexity Analysis

The time complexity of the solution is O(n^2) since the recursive function `help` is called with `n` possible values for each of the two remaining ml of soup A and soup B.

The space complexity of the solution is also O(n^2) for the memoization table `dp`.
