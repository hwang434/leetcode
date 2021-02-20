## 전화번호부
[출처](https://programmers.co.kr/learn/courses/30/lessons/42577)

![문제](/images/2020.02.20/01.png)
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