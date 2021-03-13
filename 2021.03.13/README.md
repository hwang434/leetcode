## 카펫
[출처](https://programmers.co.kr/learn/courses/30/lessons/42842)

![문제](/images/2021.03.13/01.png)


<hr>

## 내가 푼 방법
``` java
class Solution {
    public int[] solution(int brown, int yellow) {
        int[] answer = new int[2];
        int total = brown + yellow;     //노란색과 갈색 타일의 총합 갯수.

        for (int i = total - 1; i >= total/i; i--) {    //가로 길이가 더 크므로 총 타일 갯수 -1부터 시작
            if (total % i != 0 || total / i == 2) continue; //가로 세로길이로 안 나눠지거나 세로 길이가 2면
            int x = i;              //가로 길이
            int y = total / i;      //세로 길이

            int tempB = 2*x + 2*y -4;       //가로 세로 길이에 따른 갈색 타일의 갯수.
            if (tempB == brown) {           //실제 갈색 타일의 갯수와 같으면 같은 사각형 도형임.
                answer[0] = x;
                answer[1] = y;
                break;
            }
        }

        return answer;
    }
}
```

## 다른 사람이 푼 방식