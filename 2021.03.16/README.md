## 실패율
[출처](https://programmers.co.kr/learn/courses/30/lessons/42889?language=java)
## <span style='color : red; text-decoration : underline;'>주의 깊게 다시 봅시다!!</span>

![문제](/images/2021.03.16/01.png)

![문제](/images/2021.03.16/02.png)

![문제](/images/2021.03.16/03.png)


<hr>

## 내가 푼 방법
``` java
import java.util.*;

class Solution {
    public int[] solution(int N, int[] stages) {
        int[] answer = new int[N];
        HashMap hm = new HashMap<>();
        int number = stages.length;     //나눠야할 인원 수.

        for (int i = 1; i <= N; i++) {
            hm.put(i,0);
        }

        for (int key : stages) {
            if (key == N+1) continue;
            hm.put(key,(int)hm.get(key)+1);
        }

        Iterator<Integer> it = hm.keySet().iterator();

        while (it.hasNext()) {
            int stage = it.next();
            int numberOfSuccess = (int)hm.get(stage);
            double successPossible;
            if (number == 0) {
                successPossible = 0;
            } else {
                successPossible = (int)hm.get(stage) / (double)number;
            }

            hm.put(stage, successPossible);
            number -= numberOfSuccess;
        }

        int index = 0;
        while (index < N) {
            int maxIndex = method01(hm, answer);
            answer[index] = maxIndex;
            index++;
        }

        return answer;
    }

    int method01(Map<Integer, Double> map, int[] array) {
        ArrayList<Double> arrayList = new ArrayList();
        for (double value : map.values()) {
            arrayList.add(value);
        }
        Collections.sort(arrayList);
        int maxIndex = 0;

        double maxSuccessVal = arrayList.get(arrayList.size()-1);
        maxIndex = findKeyByVal(map, maxSuccessVal);
        arrayList.remove(arrayList.size()-1);

        map.remove(maxIndex);
        return maxIndex;
    }

    int findKeyByVal(Map<Integer,Double> map, double value) {
        for (int key : map.keySet()) {
            if (map.get(key) == value) return key;
        }

        return -1;
    }
}
```