## The K Weakest Rows in a Matrix
[출처](https://leetcode.com/explore/challenge/card/february-leetcoding-challenge-2021/586/week-3-february-15th-february-21st/3641/)

![문제](/images/2020.02.15/01.png)
![예제](/images/2020.02.15/02.png)


<hr>

## 내가 푼 방법
``` java

class Solution {
    public int[] kWeakestRows(int[][] mat, int k) {
        int[] answer = new int[k];          //answer array.
        HashMap<Integer, Integer> hm = new HashMap<>();

        for (int i=0; i<mat.length; i++) {
            int soldierNum = 0;
            for (int j=0; j<mat[i].length; j++) {
                if (mat[i][j] == 0) break;

                soldierNum++;
            }
            hm.put(i, soldierNum);
        }
        
        List<Integer> list = new ArrayList(hm.values());
        Collections.sort(list);
        list = list.subList(0,k);

        int key = 0;
        for (int i = 0; i<list.size(); i++) {
            key = findKeyByValue(hm,list.get(i));

            answer[i] = key;

            hm.remove(key);
        }

        return answer;
    }

    public static int findKeyByValue(Map map, int value) {
        Iterator it = map.keySet().iterator();
        int key = 0;

        while (it.hasNext()) {
            key = (int) it.next();

            if ( map.get(key).equals(value) ) {
                return key;
            }
        }

        return -1;
    }
}
```
## 풀이 훑어 보고 새로 만들어본 식.
``` java


```

## 풀고 나서 느낀 점
 - 
 - 