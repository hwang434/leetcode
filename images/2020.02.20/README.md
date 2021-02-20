## The K Weakest Rows in a Matrix
[출처](https://leetcode.com/explore/challenge/card/february-leetcoding-challenge-2021/586/week-3-february-15th-february-21st/3641/)

![문제](/images/2020.02.15/01.png)
![예제](/images/2020.02.15/02.png)


<hr>

## 내가 푼 방법
``` java
 public static boolean solution(String[] phone_book) {
        boolean answer = true;

        for (String head : phone_book) {
            for (String temp : phone_book) {
                if (temp == head) continue;
                if (checkBigger(head, temp) && head.equals(temp.substring(0,head.length()))) return false;
            }
        }
        return answer;
    }
    public static boolean checkBigger(String str1, String str2) {
        return str1.length() < str2.length();
    }

```
## 풀이 훑어 보고 새로 만들어본 식.
``` java


```

## 풀고 나서 느낀 점
 - 
 - 