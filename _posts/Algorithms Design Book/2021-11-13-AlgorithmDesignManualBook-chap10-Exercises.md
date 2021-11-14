---
layout: post
category: AlgorithmDesignBook
tags: [AlgorithmDesignBook]
title: Algorithm Design Book - Chapter 10[Exercises]
---

### Exercises

* _Consider a linear keyboard of lowercase letters and numbers, where the leftmost 26 keys are the letters A–Z in order, followed by the digits 0–9 in order, followed by the 30 punctuation characters in a prescribed order, and ended on a blank. Assume you start with your left index finger on the “A” and your right index finger on the blank._

    _Give a dynamic programming algorithm that finds the most efficient way to type a given text of length n, in terms of minimizing total movement of the fingers involved. For the text ABABABAB ...ABAB, this would involve shifting both fingers all the way to the left side of the keyboard. Analyze the complexity of your algorithm as a function of n and k, the number of keys on the keyboard._

    **Answer:**
    First we need to see why dp works here. Here the string is of length n. Take any prefix of that string of length i. If we calculated the minimum solution for that substring, one thing is certain. In that solution, one of the fingers either left or right will be on the character s[i]. we can prove this by contradiction. (try yourself)

    We can see also that the solution won't depend on the specifics of this partial solution. It only depends on the state. This is essential. Dynamic programming can be applied to any problem that obeys the _principle of optimality_.

    **3D Variant:**

    We will start with our fingers at left and right boundaries. So we can calculate cost for first character as the cost to bring that finger to that position.
    ```cpp
    // Won't be going into details of reading Input. pos is the map to
    // calculate the position for a given character.
    string s; //length N
    unordered_map<char, int> pos; // length k

    vector<vector<vector<int> > > dp(N+1, vector<vector<int> >(k, vector<int>(k, INT_MAX)));
    for(int i=0; i<k; i++){
        for(int j=0; j<k; j++){
            dp[0][i][j] = i + (k-1-j);
        }
    }

    #define abs(x) ((x)<0?-(x):(x))
    int cur;
    for(int x=0; x<N; x++){
        cur = pos[s[x]];
        for(int i=0; i<k; i++){
            for(int j=0; j<k; j++){
                dp[x+1][i][cur] = min(dp[x+1][i][cur], dp[x][i][j] + abs(j -cur));
                dp[x+1][cur][i] = min(dp[x+1][cur][i], dp[x][cur][j] + abs(i-cur));
            }
        }
    }

    return MIN(dp[N]);

    ```

    I haven't compiled this so this may need some changes. Time for some optimizations here:
    * dp[i+1] is dependent on only dp[i]. we can reduce it to a 2d array by keeping two arrays only.
    * As mentioned above, in the optimal solution for a prefix. fingers are supposed to be on the string characters at the end. Thus we can take this into consideration and convert this into 2d array.

    **2D variant**:

    Copied from here this stack Overflow [question](https://stackoverflow.com/questions/61164254/dynamic-programming-solution-to-the-shortest-distance-two-finger-typing-problem)

    ```py
    def solve(s):
    N = len(s)
    dp = [[float('inf') for x in range(26)]for x in range(N)]
    dp[0] = [0 for x in range(26)]
    for i in range(1,N):
        cur = ord(s[i])-ord('A')
        lst = ord(s[i-1])-ord('A')
        for j in range(26): # one finger currently on s[i-1], other finger on j
             dp[i][j] = min(dp[i][j], dp[i-1][j] + dist(lst,cur)) # move first finger, so second finger remains on j
             dp[i][lst] = min(dp[i][lst], dp[i-1][j] + dist(j,cur))   # move second finger, so second finger becomes the new "first finger"
             # and now the old "first finger" becomes the new "second finger"
    res = min(dp[N-1])
    return res
    ```

    If you need another optimizations, look closely. dp[i] is dependent on dp[i-1]. so we can convert it into 1d array.

