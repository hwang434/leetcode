## 완주하지 못한 선수
[출처](https://programmers.co.kr/learn/courses/30/lessons/42576)

![문제](/images/2020.03.05/01.png)


<hr>

## 내가 푼 방법
``` java
import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;
class Solution {
    public String solution(String[] participant, String[] completion) {
		HashMap<String,Integer> pMap = new HashMap<>();
        String answer;
        
        for (String partPeople : participant) {
            if (!pMap.containsKey(partPeople))
                pMap.put(partPeople, 1);
            else
                pMap.put(partPeople, pMap.get(partPeople)+1);
        }
        
        for (String complePeople : completion) {
            pMap.put(complePeople, pMap.get(complePeople)-1);
        }
        
        answer = getKeyByVal(1, pMap);
        
        return answer;
    }
    public String getKeyByVal(int peopleNum, Map<String,Integer> pMap) {
        for (String person : pMap.keySet()) {
            if (pMap.get(person) == peopleNum)
                return person;
        }
        
        return null;
    } 
}
```