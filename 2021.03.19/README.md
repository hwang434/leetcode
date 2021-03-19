## 신규 아이디 추천
[출처](https://programmers.co.kr/learn/courses/30/lessons/72410)
## <span style='color : red; text-decoration : underline;'>정규식 더 이상 미루지 말고 공부하자..</span>

![문제](/images/2021.03.19/01.png)

![문제](/images/2021.03.19/02.png)

![문제](/images/2021.03.19/03.png)


<hr>

## 내가 푼 방법
``` java
    import java.util.ArrayList;
class Solution {
    public String solution(String new_id) {
        String answer = "";
//        1단계 new_id의 모든 대문자를 대응되는 소문자로 치환합니다.
        StringBuilder sb = new StringBuilder(new_id.toLowerCase());
//        2단계 new_id에서 알파벳 소문자, 숫자, 빼기(-), 밑줄(_), 마침표(.)를 제외한 모든 문자를 제거합니다.
        for (int charIdx = 0; charIdx < sb.length(); charIdx++) {
            char c = sb.charAt(charIdx);
            if (!(Character.isDigit(c) || c == '-' || c == '_' || c == '.' || ('a' <= c && c <='z'))) {
                sb.deleteCharAt(charIdx);
                charIdx--;
            }
        }
        System.out.println("2단계 끝 : "+sb.toString());
        //        3단계 new_id에서 마침표(.)가 2번 이상 연속된 부분을 하나의 마침표(.)로 치환합니다.
        int fromIndex = 0;
        int idxOfPoint = sb.indexOf(".",fromIndex);
        while (idxOfPoint != -1) {
            if (idxOfPoint == sb.length() - 1) {
                break;
            }
            if (sb.charAt(idxOfPoint+1) == '.') {
                sb.deleteCharAt(idxOfPoint+1);
            } else {
                fromIndex = idxOfPoint + 1;
            }
            idxOfPoint = sb.indexOf(".",fromIndex);
        }

        System.out.println("3단계 끝 : "+sb.toString());

        //        4단계 new_id에서 마침표(.)가 처음이나 끝에 위치한다면 제거합니다.
        if (sb.charAt(0) == '.') {
            sb.deleteCharAt(0);
        }
        if (sb.length()-1 >= 1 ) {
            if (sb.charAt(sb.length()-1) == '.') {
                sb.deleteCharAt(sb.length()-1);
            }
        }
        System.out.println("4단계 끝 : "+sb.toString());
        //        5단계 new_id가 빈 문자열이라면, new_id에 "a"를 대입합니다.
        if (sb.toString().equals("")) {
            sb.append("a");
        }
//        6단계 new_id의 길이가 16자 이상이면, new_id의 첫 15개의 문자를 제외한 나머지 문자들을 모두 제거합니다.
        if (sb.length() >= 16) {
            sb = new StringBuilder(sb.subSequence(0,15));
        }
//                만약 제거 후 마침표(.)가 new_id의 끝에 위치한다면 끝에 위치한 마침표(.) 문자를 제거합니다.
        if (sb.charAt(sb.length()-1) == '.') {
            sb.deleteCharAt(sb.length()-1);
        }
//        7단계 new_id의 길이가 2자 이하라면, new_id의 마지막 문자를 new_id의 길이가 3이 될 때까지 반복해서 끝에 붙입니다.
        if (sb.length() <= 2) {
            char lastChar = sb.charAt(sb.length()-1);
            do {
                sb.append(lastChar);
            } while (sb.length() < 3);
        }

        answer = new String(sb.toString());
        return answer;
    }
}


```

``` java
class Solution {
    public String solution(String new_id) {
        String answer = "";
        String temp = new_id.toLowerCase();

        temp = temp.replaceAll("[^-_.a-z0-9]","");
        System.out.println(temp);
        temp = temp.replaceAll("[.]{2,}",".");
        temp = temp.replaceAll("^[.]|[.]$","");
        System.out.println(temp.length());
        if(temp.equals(""))
            temp+="a";
        if(temp.length() >=16){
            temp = temp.substring(0,15);
            temp=temp.replaceAll("^[.]|[.]$","");
        }
        if(temp.length()<=2)
            while(temp.length()<3)
                temp+=temp.charAt(temp.length()-1);

        answer=temp;
        return answer;
    }
}
```

정규식 빨리하자!!!!!!!!!!!!!!!!!!!!!!!