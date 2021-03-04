## 위장
[출처](https://programmers.co.kr/learn/courses/30/lessons/42578?language=java)

![문제](/images/2020.03.04/01.png)
<hr>

## 내가 푼 방법
``` java
public int solution(String[][] clothes) {
    int answer = 1;
    HashMap<String, Integer> spy = new HashMap<>();     //key는 옷의 종류 value는 옷의 갯수.

    for (String[] cloth : clothes) {        //가지고 있는 모든 옷의 종류를 key로 등록함.
        spy.put(cloth[1], 0);
    }

    for (String[] cloth : clothes) {        //같은 옷이 나오면 갯수를 추가해줌.
        int temp = spy.get(cloth[1]);
        spy.put(cloth[1], ++temp);
    }

    for (int clothNum : spy.values()) {
        answer *= ++clothNum;
    }
    --answer;

    return answer;
}
```

## 풀고 나서 정리한 거

``` java
public static int solution(String[][] clothes) {
    int answer = 1;
    HashMap<String, Integer> spy = new HashMap<>();     //key는 옷의 종류 value는 옷의 갯수.

    for (String[] cloth : clothes) {        //옷의 종류와 갯수를 등록해주는 반복문.
        if (!spy.containsKey(cloth[1])) spy.put(cloth[1], 1);   //처음 나오는 옷 종류면 1개로 등록해줌.
        else spy.put(cloth[1], spy.get(cloth[1])+1);    //이미 나왔던 옷 종류면 갯수를 1개 추가헤줌.
    }

    for (int clothNum : spy.values()) {     //입은 경우 안 입은 경우 모든 경우의 수 구하는 반복문.
        answer *= ++clothNum;
    }

    --answer;       //하나도 안 입었을 경우의 수 1을 빼줌.

    return answer;
}

```