---
layout: post
title: level 1. 완주하지 못한 선수
category: codingTest
permalink: /algorithm/:year/:month/:day/:title/
tags: [codingTest, Java]
comments: true
---
# level 1. 완주하지 못한 선수
> 출처 : https://programmers.co.kr/learn/courses/30/lessons/42576?language=java

## Question

## Solution1
```java
import java.util.HashMap;

class Solution {
    public String solution(String[] participant, String[] completion) {
        String answer = "";
        HashMap<String, Integer> hm = new HashMap<>();
        for (String player : participant) hm.put(player, hm.getOrDefault(player, 0) + 1);
        for (String player : completion) hm.put(player, hm.get(player) - 1);

        for (String key : hm.keySet()) {
            if(hm.get(key) != 0 {
                hm.get(key) != 0) {
                    answer = key;
                }
            }
        }
        return answer;
    }
}
```

## Solution2
```java
import java.util.*;
class Solution {
    public String solution(String[] participant, String[] completion) {
        Arrays.sort(participant);
        Arrays.sort(completion);
        int i;
        for ( i=0; i<completion.length; i++){

            if (!participant[i].equals(completion[i])){ // equals는 문자열의 값을 비교하고 != 연산자는 주소값을 비교합니다.
                return participant[i];
            }
        }
        return participant[i];
    }
}

```

## lesson
