## Number of 1 Bits
[출처](https://leetcode.com/explore/challenge/card/february-leetcoding-challenge-2021/584/week-1-february-1st-february-7th/3625/)

![](/images/2020.02.01/01.png)
<hr>

## 내가 푼 방법

``` java
public class Solution {
    // you need to treat n as an unsigned value
    public static int hammingWeight(int n) {
        String str = Integer.toBinaryString(n);
        int count = 0;

        for (int i=0; i<str.length(); i++) {
            if (str.charAt(i) == '1') count++;
            
        }

        return count;
    }
}
```

## 엄청 간결하면서 간단한 방법

``` java
public class Solution {
    public static int hammingWeight(int n) {
        return Integer.bitCount(n);
    }
}
```

## 이해가 잘 안 가는 코드

``` java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int bits = 0;
        int mask = 1;
        for (int i = 0; i < 32; i++) {
            if ((n & mask) != 0) {
                bits++;
            }
            mask <<= 1;
        }
        return bits;
    }
}
```
<hr>

## 다른 풀이 보고 느낀 점
 - bit 연산 공부 좀 해야겠다.

