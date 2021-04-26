---
layout: post
title: Favorite Problems From CF 2020
---

2020 was an eventful year for competitive programming for me, especially on CodeForces.

In terms of rating, I have accumulated a maximum rating of 2499 and have reached the title Grandmaster and International Master during the 2nd half of the year and was a stable Master for the 1st half of the year.
Compared to 2019, where I initially dropped from Candidate Master to Expert and later stayed at Master, I am very satisfied with my rating progress in 2020.

As for submissions, I have made 2220 submissions and among them, I solved 655 problems. Also, I participated in 24 contest officially on Codeforces.

The primary reason that I wanted to write this blog is to share some of my favorite problems that I solved on Codeforces in 2020.
When thinking about what were my favorite problems of the year I accounted for the impact it had on me and the elegance of the solution.
There were simply too many problems that I enjoyed solving this year, but I managed to compile a list of 37 problems and cut it down to the 10 best problems.
First I'll list in the order I solved them in for the honorable mention problems that made it to the 37 problem cut and then I will show and explain the best 11.

<h3 align = "center"> Honorable Mention </h3>

- [NN County](https://codeforces.com/contest/983/problem/E)
- [The Untended Antiquity](https://codeforces.com/contest/869/problem/E)
- [Recursive Queries](https://codeforces.com/contest/1117/problem/G)
- [Too Much Money](https://codeforces.com/contest/725/problem/E)
- [Water Balance](https://codeforces.com/contest/1299/problem/C)
- [T-Shirt](https://codeforces.com/contest/758/problem/E)
- [Magical Permutation](https://codeforces.com/contest/1163/problem/E)
- [Selling Souvenirs](https://codeforces.com/contest/808/problem/E)
- [You Are Given A Tree](https://codeforces.com/contest/1039/problem/D)
- [Exam Cheating](https://codeforces.com/contest/796/problem/E)
- [Ski Accidents](https://codeforces.com/contest/1368/problem/E)
- [The Hidden Pair](https://codeforces.com/contest/1370/problem/F2)
- [Sky Full Of Stars](https://codeforces.com/contest/997/problem/C)
- [Pointer Ordering](https://codeforces.com/contest/1254/problem/C)
- [Rearrange](https://codeforces.com/contest/1383/problem/D)
- [Treeland And Viruses](https://codeforces.com/contest/1320/problem/E)
- [Tree Modification](https://codeforces.com/contest/1375/problem/G)
- [World Of Darkraft - 2](https://codeforces.com/contest/464/problem/D)
- [New Year And Cleaning](https://codeforces.com/contest/611/problem/F)
- [U2](https://codeforces.com/contest/1142/problem/C)
- [Winding Polynomial Line](https://codeforces.com/contest/1158/problem/D)
- [The Hardwork Of The Paparazzi](https://codeforces.com/contest/1427/problem/C)
- [Allowed Letters](https://codeforces.com/contest/1009/problem/G)
- [Nullify The Matrix](https://codeforces.com/contest/1451/problem/F)
- [Sum](https://codeforces.com/contest/1442/problem/D)
- [Errich Tac Toe](https://codeforces.com/contest/1450/problem/C2)

<h3 align = "center"> Top 11 </h3>

1. <u> Subset With Zero Sum

    [Problem Link](https://codeforces.com/contest/1270/problem/G), Difficulty: 2700
    <details>
        <summary> Solution </summary>
        $$i-n \le a_i \le i-1$$
        $$-n \le a_i-i \le -1$$
        $$n \ge i-a_i \ge 1$$
        This means that $i-a_i = j$ where $1 \le j \le n$ is another index.
        Now consider the graph where edges are drawn between $i$ and $i - a_i$. Note that this is a functional graph, meaning that there exists an oriented cycle.
        Now consider all the nodes in an oriented cycle $\{i_1, i_2, i_3, \ldots, i_k, i_1\}$.
        Summing each distinct node in the sequence, we get
        $$\sum_{i = 1}^k i_k = \sum_{i = 1}^k i_k - a_{i_k}$$
        Subtracting $i_k$ on both side, yields
        $$0 = \sum_{i = 1}^k -a_{i_k} \implies 0 = a_1 + \ldots + a_k$$
        Thus, we reduced the problem to finding an oriented cycle in a functional graph, which can be solved using DFS or Floyd's Cycle Detection Algorithm.
    </details>

2. <u> Awesome Substring </u>

    [Problem Link](https://codeforces.com/contest/1270/problem/F), Difficulty: 2600
    <details>
        <summary> Solution </summary>
        Think about the string as an array of integers instead ('0' turns into value 0 and similar for '1').
        Compute the prefix sum and call it $pre$ where $pre[i]$ represents the sum of the first $i$ elements.
        Now we can state the condition as count the number of subarrays $(l, r)$ such that
        $$pre[r] - pre[l - 1] | r - l + 1$$
        In other words, we can count the number of unordered pairs $(l, r)$ such that there exists some $k \in \mathbb{Z}$ such that
        $$k * (pre[r] - pre[l - 1]) = r - l + 1$$
        Since $r - l + 1$ is bounded by $N$, then either $k$ or $pre[r] - pre[l - 1]$ is less than or equal to $\sqrt{N}$.

        If $k$ is less than or equal to $\sqrt{N}$, then rearranging can get that
        $$k * pre[r] - r = k * pre[l - 1] - k * (l - 1)$$
        So, for each $k$ we can maintain a frequency array of $k * pre[i] - i$ for every $i$ and then we can use $(fre[v] * fre[v - 1]) / 2$ for every non-zero $v$;

        If $pre[r] - pre[l - 1] \le \sqrt{N}$, then for every $r$ group each $l$ into group of $1 \le g \le \sqrt{N}$ such that $pre[r] - pre[l-1] = g$.
        Notice that each group is contiguous and let it be $[a_g, b_g]$.
        Fixing $g$ allows us to calculate how many $g | r - l + 1$ where $l \in [a_g, b_g]$.
        This is the same to count the number of $l$ such that $r$ is congruent to $l-1$ in modulo $g$.

        Note that when implementing be careful to not overcount subarrays where it satisfies both conditions.
        One method to avoid that is to subtract those subarrays by using PIE, but I find that to be slow in practice.
        Another method is to count those that satisfy the first condition and then count subarrays who satisfy the second but not the first condition or vice versa.

        Since, each pass is $\mathcal(O)(N\sqrt{N}), then it should pass within the time limits.
        However, I find that the time limit is tight.
        One optimization is to use a 100 million sized int array for the frequency array.
    </details>

3. <u> Varying Kbits </u>

    [Problem Link](https://codeforces.com/contest/772/problem/D), Difficulty: 2700

4. <u> Secure Password </u>

    [Problem Link](https://codeforces.com/contest/1365/problem/G), Difficulty: 2800

5. <u> Crossword Expert </u>

    [Problem Link](https://codeforces.com/contest/1194/problem/F), Difficulty: 2400

6. <u> Souvenirs </u>

    [Problem Link](https://codeforces.com/contest/765/problem/F), Difficulty: 3100

7. <u> Almost All </u>

    [Problem Link](https://codeforces.com/contest/1205/problem/D), Difficulty: 2700

8. <u> Change Free </u>

    [Problem Link](https://codeforces.com/contest/767/problem/E), Difficulty: 2400

9. <u> Double Knapsack </u>

    [Problem Link](https://codeforces.com/contest/618/problem/F), Difficulty: 3000

10. <u> Reality Show </u>

    [Problem Link](https://codeforces.com/contest/1322/problem/D), Difficulty: 2800

11. <u> Roads And Ramen </u>

    [Problem Link](https://codeforces.com/contest/1434/problem/D), Difficulty: 2800



[//]: # 'Next you can update your site name, avatar and other options using the _config.yml file in the root of your repository (shown below).'

[//]: # '![_config.yml]({{ site.baseurl }}/images/config.png)'

[//]: # 'The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.'
