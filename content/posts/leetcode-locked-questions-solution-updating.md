---
title: "Leetcode Locked Questions Solution (Updating)"
date: 2022-07-21T16:58:55+10:00
lastmod: 
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