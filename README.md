# LeetCode-91.-Decode-Ways

class Solution:
    def numDecodings(self, s: str) -> int:
        def convert(s):
            l = list('abcdefghijklmnopqrstuvwxyz')
            d = {x: c for c, x in enumerate(l, start=1)}
            q = sum((26 ** (c - 1)) * d[s[x]]
                    for c, x in enumerate(range(len(s) - 1, -1, -1), start=1))
            return q

        if not s or s[0] == '0':
            return 0
        dp = [0]*(len(s)+1)
        dp[0] = 1
        dp[1] = 1 if s[0] != 0 else 0

        for x in range(2, len(s)+1):
            if 1 <= int(s[x-1]) <= 9:
                dp[x] += dp[x-1]
            if 10 <= int(s[x-2:x]) <= 26:
                dp[x] += dp[x-2]
        return dp[len(s)]
