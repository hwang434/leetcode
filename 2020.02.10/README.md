## Number of 1 Bits
[출처](https://leetcode.com/explore/challenge/card/february-leetcoding-challenge-2021/585/week-2-february-8th-february-14th/3635/)

![문제](/images/2020.02.10/01.png)
![예제](/images/2020.02.10/02.png)
![제한조건](/images/2020.02.10/03.png)


<hr>

## 내가 푼 방법
``` java

/*
// Definition for a Node.
class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
*/

class Solution {
    public Node copyRandomList(Node head) {
            if (head == null) return null;
            else if (head.next == null) {
                Node answer = new Node(head.val);
                
                if (head.random == null) return answer;
                answer.random = answer;
                
                return answer;
            }
            ArrayList<Node> originNodeList = new ArrayList<>();
            ArrayList<Node> cloneNodeList = new ArrayList<>();

            Node temp = head;
            Node cloneTemp = new Node(temp.val);

            do {
                originNodeList.add(temp);

                cloneTemp.next = new Node(temp.next.val);

                cloneNodeList.add(cloneTemp);

                temp = temp.next;
                cloneTemp = cloneTemp.next;
            } while (temp.next != null);
            originNodeList.add(temp);
            cloneNodeList.add(cloneTemp);

            for (int i=0; i<originNodeList.size(); i++) {
                if (head.random == null) {
                    head = head.next;
                    continue;
                }
                cloneNodeList.get(i).random = cloneNodeList.get(originNodeList.indexOf(head.random));
                head = head.next;
            }

            return cloneNodeList.get(0);
    }
}
```

## 풀고 나서 느낀 점
 - 원래 HashMap을 사용해볼 생각을 하긴 했는데, 발상의 전환이 부족했다.
 - 너무 하드 코딩했다. 여러 가지 방식으로 다시 풀어볼 것.