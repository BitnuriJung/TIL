
# Codility Time Complexity
## FrogJmp

<br/>

### 첫번째 풀이 
- X -> Y 로 이동해야 하고, 한 번에 D만큼 갈 때, 최소 몇 번을 이동해야 하는지 return
```java script
    function solution(X, Y, D) {
        // write your code in JavaScript (Node.js 14)

        let count = 0;
        let left_distance = Y - X;

        console.log('left distance :'+ left_distance);

        while(left_distance>0){
            left_distance = left_distance - D;
            count++;
            console.log("남은 거리 = "+left_distance);
        }

        return count;

    }
```
- **O(Y-X) 의 시간복잡도** : Y가 X나 D에 비해 월등히 클 때, 타임아웃 에러가 발생함
- 정확도 100, 퍼포먼스 20으로 55% 획득

<br/>


### 두번째 풀이 
```java script
    function solution(X, Y, D) {
    // write your code in JavaScript (Node.js 14)
    
        let left_distance = Y - X;

        let count = parseInt(left_distance/D);
        // console.log('count : '+count);

        if(left_distance%D!==0){
            count++;
        // console.log('left!!! count should be : '+count);

        }

        return count;
}
```
- **O(1) 시간복잡도**
- 정확도 75, 퍼포먼스 100, 총점 88
- 한 번에 크게 점프한다고 쳤을 때, 1이 나와야 하는데 2가 나와버리는 에러 (giant big step 문제) 가 난다는데 무슨 상황인지 모르겠다....

<br/>


### 남의 답을 참고한 세번째 풀이

```java script
    function solution(X, Y, D) {
    // write your code in JavaScript (Node.js 14)
    
       let count = Math.floor( (Y-X) / D);
        // console.log('count : '+count);

        if( (Y-X) % D !== 0){
            count++;
        // console.log('left!!! count should be : '+count);

        }

        return count;
}
```
- :confused: 새로운 변수 선언 -> 있는 변수 그대로 사용.
    - 가독성이 별로인 것 같은데 대부분의 답변들이 변수를 그대로 사용한다. 메모리 낭비를 막기 위한걸까?
- 맨 첫 count 부분에 `parseInt()` 로 감쌌던 부분을 `Math.floor()`로 변경하니 100점이 나왔다. 
    - :confused:`parseInt`와 `Math.floor`는 무슨 차이인거지? 
    - 둘의 차이는 처리하는 값이 **음수일 때** 나타난다. parseInt는 소수점을 버리고 Math.floor는 내림을 사용한다! 
    - 양수일 때는 둘 다 내림
        ```
        c = Math.floor( "-12.34" ); // -13
        d = Math.floor( "-56.78" ); // -57

        c2 = parseInt( "-12.34" ); // -12
        d2 = parseInt( "-56.78" ); // -56
        ``` 
        - 출처 : [[Javascript] parseInt()과 Math.floor()의 차이](https://velog.io/@mnmm/js-parseint-mathfloor)
        - 하지만 우리 조건에서 X는 Y보다 작거나 같기 때문에 음수 값이 들어갈 일이 없는데?
        - 코딜리티에다가 문의를 하고 싶다.. input 값을 줘보세요 ㅠㅠ 

<br/>

### 문제 전문
```
A small frog wants to get to the other side of the road. The frog is currently located at position X and wants to get to a position greater than or equal to Y. The small frog always jumps a fixed distance, D.

Count the minimal number of jumps that the small frog must perform to reach its target.

Write a function:

class Solution { public int solution(int X, int Y, int D); }

that, given three integers X, Y and D, returns the minimal number of jumps from position X to a position equal to or greater than Y.

For example, given:

  X = 10
  Y = 85
  D = 30
the function should return 3, because the frog will be positioned as follows:

after the first jump, at position 10 + 30 = 40
after the second jump, at position 10 + 30 + 30 = 70
after the third jump, at position 10 + 30 + 30 + 30 = 100
Write an efficient algorithm for the following assumptions:

X, Y and D are integers within the range [1..1,000,000,000];
X ≤ Y.
Copyright 2009–2022 by Codility Limited. All Rights Reserved. Unauthorized copying, publication or disclosure prohibited.
```