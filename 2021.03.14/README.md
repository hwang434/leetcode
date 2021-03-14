## 스킬트리
[출처](https://programmers.co.kr/learn/courses/30/lessons/49993)

![문제](/images/2021.03.14/01.png)


<hr>

## 내가 푼 방법
``` java
import java.util.ArrayDeque;
import java.util.Queue;

class Solution {
    public int solution(String skill, String[] skill_trees) {   //skill : 시스템에서 정한 스킬트리, skill_trees : 유저가 원하는 스킬트리들.
        int answer = 0;                                     //가능한 스킬트리 갯수.
        Queue<Character> skillQueue = null;                 //가능한 스킬트리를 담을 큐 변수.

        for (String skill_tree : skill_trees) {     //유저가 원하는 스킬트리 갯수만큼 반복문을 돔.
            skillQueue = makeQueue(skillQueue, skill);
            boolean isTrue = true;

            for (char s : skill_tree.toCharArray()) {
                if ( isMatchedSkill(skillQueue, s) ) {
                    continue;
                }
                else {
                    isTrue = false;
                    break;
                }
            }

            if (isTrue) answer++;
        }
        return answer;
    }

    public Queue<Character> makeQueue(Queue<Character> skillQueue, String skill) {      //Queue를 매번 새로 만드는 메서드.
        skillQueue = new ArrayDeque<>();

        for (char c : skill.toCharArray()) {
            skillQueue.add(c);
        }

        return skillQueue;
    }

    public boolean isMatchedSkill(Queue<Character> skill,char s) {        //skill : 가능한 스킬트리, s : 유저가 원하는 스킬 트리에서 뽑아온 스킬 한개.
        if ( !skill.contains(s) ) return true;      //만약 유저가 원하는 스킬 한 개가 시스템에서 정한 스킬트리에 없으면

        if ( skill.poll().equals(s) ) return true;
        else return false;
    }
}
```

## 다른 사람이 푼 방식
``` java
import java.util.*;

class Solution {
    public int solution(String skill, String[] skill_trees) {
        int answer = 0;
        ArrayList<String> skillTrees = new ArrayList<String>(Arrays.asList(skill_trees));
        //ArrayList<String> skillTrees = new ArrayList<String>();
        Iterator<String> it = skillTrees.iterator();

        while (it.hasNext()) {
            if (skill.indexOf(it.next().replaceAll("[^" + skill + "]", "")) != 0) {
                it.remove();
            }
        }
        answer = skillTrees.size();
        return answer;
    }
}
```
``` java
class Solution {
    public int solution(String skill, String[] skill_trees) {
        int answer = 0;
        for (String skillTree : skill_trees) {
            int learningIdx = 0;
            boolean isAble = true;
            for (char curSkill : skillTree.toCharArray()) {
                int skillIdx = skill.indexOf(curSkill);
                if (skillIdx == -1)
                    continue;
                else if (skillIdx == learningIdx)
                    learningIdx++;
                else {
                    isAble = false;
                    break;
                }
            }
            if (isAble)
                answer++;
        }
        return answer;
    }
}
```
