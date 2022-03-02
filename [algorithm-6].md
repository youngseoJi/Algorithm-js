## [Algorithm] - 문자열압축, 반복되는 문자와 반복 횟수 나열하기

---



>**문제 : 같은 문자가 연속으로 반복되는 경우 해당문자 오른쪽에 반복 횟수를 표기하여 문자열을 압축해라. (반복되지않는 문자는 횟수 표시생략, 대문자 문자열이 주어진 상탠)**

## 풀이

1. 반복되는 문자개수를 셀 변수 count에 1을 할당하고, (무조건 1개 부터시작해서 1을 초기화 값으로 준 것)
 결과 문자열을 담을 변수 result 선언 하고 빈문자열을 할당한다.
2. 문자열을 조회한다. -> for문
3. str[i]해당 문자를 빈 배열에 담아준다.
4. 직전문자와 현재문자가 같을경우 count +1을 증가시키고
5. 같지않은 경우 빈문자열에 해당 인덱스 요소와 count 값을 담는다. 
6. result에 1을 제거하기위해 문자열요소가 1이 아닌 경우만 다른 변수에 담아준다.

>- 선생님 풀이와 다른 점은 선생님은 count 가 1보다 클경우만 문자열에 담아주는 조건을 걸었다. <- 이게 훨 깔끔
>그리고 " "빈문자열을 맨 뒤에 추가하셨는데 안해도 되는 부분이였다.

```js
// 내 코드
      function solution(str) {
        let result = "";
        let count = 1;
        for (let i = 0; i < str.length; i++) {
          if (str[i] === str[i + 1]) {
            count++;
          } else {
            result += str[i];
            result += count;
            count = 1;
          }
        }
        let end = "";
        for (let el of result) {
          if (el !== "1") {
            end += el;
          }
        }
        return end;
      }

      let str = "KKHSSSSSSSE";
      console.log(solution(str)); //K2HS7E
```
### 선생님 풀이 추가한 버전
```js

  function solution(str) {
        let result = "";
        let count = 1;
        for (let i = 0; i < str.length; i++) {
          if (str[i] === str[i + 1]) {
            count++;
          } else {
            result += str[i];
            if (count > 1) {
              result += count;
            }
            count = 1;
          }
        }
        return result;
      }

      let str = "KKHSSSSSSSE";
      console.log(solution(str)); //K2HS7E
```