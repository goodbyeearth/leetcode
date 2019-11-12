# [204.Count Primes](https://leetcode.com/problems/count-primes/)

# 思路1
那么，如果先尝试2，然后再针对 3 到√x 的所有奇数进行试除，是不是就足够优了捏？答案显然是否定的嘛？写到这里，才刚开始热身哦。
一些更加聪明的程序猿，会发现一个问题：尝试从 3 到√x 的所有奇数，还是有些浪费。比如要判断101是否质数，101的根号取整后是10，那么，按照境界4，需要尝试的奇数分别是：3，5，7，9。但是你发现没有，对9的尝试是多余的。不能被3整除，必然不能被9整除......顺着这个思路走下去，这些程序猿就会发现：其实，只要尝试小于√x 的质数即可。而这些质数，恰好前面已经算出来了（是不是觉得很妙？）。
所以，处于这种境界的程序猿，会把已经算出的质数，先保存起来，然后用于后续的试除，效率就大大提高了。
顺便说一下，这就是算法理论中经常提到的：以空间换时间。

```c++
class Solution {
public:
    int countPrimes(int n) {
        if(n<=2)
            return 0;

        int count_prime = 1;
        vector<int> prime;
        bool is_prime;
        
        prime.push_back(2);
        for(int i=3;i<n;i+=2){
            is_prime = true;
            for(int j=0;j<count_prime && prime[j]<=sqrt(i);j++)
                if(i%prime[j]==0){
                    is_prime = false;
                    break;
                }
            if(is_prime){
                count_prime++;
                prime.push_back(i);
            }
        }
        return count_prime;
    }
};
```

# 思路2
筛法。