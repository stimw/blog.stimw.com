---
title: "Leetcode Locked Questions Solution (Updating)"
date: 2022-07-21T16:58:55+10:00
lastmod: 2022-07-22
draft: false

images: []
tags: ['Leetcode', 'Algorithm']
categories: ["Dev"]
series: []
series_weight:
seriesNavigation:
featuredImage: ""
featuredImagePreview: ""

hiddenFromHomePage: false
rssFullText: false
---

## 256. Paint House

```python
class Solution:
    """
    @param costs: n x 3 cost matrix
    @return: An integer, the minimum cost to paint all houses
    """
    def min_cost(self, costs: List[List[int]]) -> int:
        n = len(costs)
        f = [[float("inf") for _ in range(3)] for _ in range(n+1)]

        #init 
        f[0][0] = f[0][1] = f[0][2] = 0
        # i is the ith house
        for i in range(1, n+1):
            # j is the color of the (i-1)th house
            for j in range(0, 3):
                # k is the color of the (i-2)th house
                for k in range(0, 3):
                    if j == k:
                        continue
                    if f[i-1][k] + costs[i-1][j] < f[i][j]:
                        f[i][j] = f[i-1][k] + costs[i-1][j]

        res = min(f[n][0], f[n][1], f[n][2])
        return res
```

## 361. Bomb Enemy
```python
class Solution:
    """
    @param grid: Given a 2D grid, each cell is either 'W', 'E' or '0'
    @return: an integer, the maximum enemies you can kill using one bomb
    """
    def max_killed_enemies(self, grid: List[List[str]]) -> int:
        m = len(grid)
        if m == 0:
            return 0
        n = len(grid[0])
        dp = [[0 for _ in range(n)] for _ in range(m)]
        res = [[0 for _ in range(n)] for _ in range(m)]

        # up
        for i in range(m):
            for j in range(n):
                if grid[i][j] == 'W':
                    dp[i][j] = 0
                else:
                    dp[i][j] = 0
                    if grid[i][j] == 'E':
                        dp[i][j] = 1
                    if (i - 1 >= 0):
                        dp[i][j] += dp[i-1][j]
                        
                res[i][j] += dp[i][j]
        
        # down
        for i in range(m-1, -1, -1):
            for j in range(n):
                if grid[i][j] == 'W':
                    dp[i][j] = 0
                else:
                    dp[i][j] = 0
                    if grid[i][j] == 'E':
                        dp[i][j] = 1
                    if (i + 1 < m):
                        dp[i][j] += dp[i+1][j]
                        
                res[i][j] += dp[i][j]

        # left
        for i in range(m):
            for j in range(n):
                if grid[i][j] == 'W':
                    dp[i][j] = 0
                else:
                    dp[i][j] = 0
                    if grid[i][j] == 'E':
                        dp[i][j] = 1
                    if (j - 1 >= 0):
                        dp[i][j] += dp[i][j-1]
                        
                res[i][j] += dp[i][j]

        # right
        for i in range(m):
            for j in range(n-1, -1, -1):
                if grid[i][j] == 'W':
                    dp[i][j] = 0
                else:
                    dp[i][j] = 0
                    if grid[i][j] == 'E':
                        dp[i][j] = 1
                    if (j + 1 < n):
                        dp[i][j] += dp[i][j+1]
                        
                res[i][j] += dp[i][j]

        result = 0
        for i in range(m):
            for j in range(n):
                if grid[i][j] == '0' and res[i][j] > result:
                    result = res[i][j]
        
        for i in range(m):
            print(res[i])

        return result
```