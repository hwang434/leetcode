## 다트 게임
[출처](https://programmers.co.kr/learn/courses/30/lessons/17682?language=java)
## <span style='color : red; text-decoration : underline;'>답지 보고 비교해보자. 엄청 오래 걸리고, 코드도 드럽게 나옴.</span>

![문제](/images/2021.03.18/01.png)

![문제](/images/2021.03.18/02.png)

![문제](/images/2021.03.18/03.png)


<hr>

## 내가 푼 방법
``` java
    import java.util.ArrayList;

class Solution {
    public int solution(String dartResult) {
        int answer;
        StringBuilder sb = new StringBuilder();
        char[] charArray = dartResult.toCharArray();

        //1D2S0T
        for (int i = 0; i< charArray.length; i++) {
            char c = charArray[i];
            if (i == charArray.length-1) {
                sb.append(c);
                break;
            }
            if ('0' <= c && c <= '9') {
                sb.append(c);
                continue;
            } else if (c == 'S' || c == 'D' || c == 'T') {
                if (i+1 < charArray.length) {
                    if (Character.isDigit(charArray[i+1])) {
                        sb.append(c);
                        sb.append(' ');
                    } else if (charArray[i+1] == '#' || charArray[i+1] == '*') {
                        sb.append(c);
                    }
                }
                continue;
            }
            switch (c) {
                case '#' :  sb.append(c);
                            sb.append(' ');
                            break;
                case '*' :  sb.append(c);
                            sb.append(' ');
                            break;
            }
        }

        String str = new String(sb.toString());
        String[] strArray = str.split(" ");

        ArrayList<Integer> arrayList = new ArrayList<>();

        for (int i = 0; i < strArray.length; i++) {
            sb = new StringBuilder(strArray[i]);
            int lastIndex = sb.length()-1;
            char lastChar = sb.charAt(lastIndex);
            int score;

            if (lastChar == 'S' || lastChar == 'D' || lastChar == 'T') {
                score = setScoreAlphabet(sb.charAt(sb.length()-1), arrayList, sb, sb.length()-1);
                arrayList.add(score);
            } else if (lastChar == '*' || lastChar == '#') {
                if (lastChar == '*') {
                    sb.deleteCharAt(lastIndex);
                    score = setScoreAlphabet(sb.charAt(sb.length()-1),arrayList,sb,lastIndex-1);
                    arrayList.add(score*2);
                    if (i != 0) {
                        arrayList.set(i-1, arrayList.get(i-1)*2);
                    }
                } else if (lastChar == '#') {
                    sb.deleteCharAt(lastIndex);
                    score = setScoreAlphabet(sb.charAt(sb.length()-1),arrayList,sb,lastIndex-1);
                    arrayList.add(-score);
                }
            }
        }
        int sum = 0;
        for (int score : arrayList) {
            sum += score;
        }

        return sum;
    }
    public int setScoreAlphabet(char lastChar, ArrayList<Integer> arrayList,StringBuilder sb,int lastIdx) {
        sb.deleteCharAt(lastIdx);
        int score = Integer.parseInt(sb.toString());
        switch (lastChar) {
            case 'D' :  score = (int)Math.pow(score,2);
                break;
            case 'T' :  score = (int)Math.pow(score,3);
                break;
        }
        return score;
    }
}

```