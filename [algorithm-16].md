## [algorithm/ 자료구조 스택 (stack) ] 괄호 내의 문자만 제거하기

---

> **문제 : () 안의 문자를 제거하고 남은 문자만 출력해라**

### 어려웠던 점
- 조건 - 조회한 문자가 ) 닫는 괄호인 경우, else 문 내부에 따로 while문으로 사용하는 것을 생각 못했다. 
**while문은 false일때 종료, 탈출**한다. (제거한 요소가 "(" 인경우 탈출조건 설정)
```js
while(stack.pop() !== "(");
```
**stack [ ] 의 가장 최근 요소부터 반복해서 제거하다, 제거된 요소가 "(" 여는 괄호인 경우 바로 while문 탈출! => 괄호내의 문자부터 "(" 여는 괄호까지 제거**하는 부분을 작성하는 부분!

 

## 접근방법 
- **스택 자료구조** 방법으로 접근, 배열 []에 ( 여는괄호와 문자를 순서대로 차곡차곡 담는다.
- 이때, ) 닫는 괄호를 만나면 최근에 들어간 요소 (오른쪽 요소 부터)부터 제거하며 해당 괄호의 짝인 ( 여는 괄호를 까지 제거한다.
      
## 풀이
1. stack 데이터를 담을 변수와 빈배열 []을 할당한다.
2. for문으로 순서대로 모든 문자를 조회한다.
3. if 조건 1) 조회한 문자가 ) 가 아닌경우, stack []에 push() 문자를 담는다. 
4. else 조건 2) 조회한 문자가 ) 인 경우, 
4-1. 내부에 while문으로 stack [] 의 요소를 반복해서 제거한다.
 stack.pop()!== "(" 제거한 요소가 여는 괄호인 경우 while문 종료한다.
5. 다시 for문 으로 조회하며, 반복한다.
5. for문 반복종료 후, stack에 남은 요소를 .join() 문자열로 변환하여 출력한다.

```js      
function solution(str) {
    let stack = [];

    for (let i = 0; i < str.length; i++) {
    	if (str[i] !== ")") {
            stack.push(str[i]);
        } 
        else {
          while(stack.pop() !== "(") ;
        }
      }
      stack = stack.join()
      return stack;
    }

    let str = "(A(BC)D)EF(G(H)(IJ)K)LM(N)";
    console.log(solution(str)); // E,F,L,M
```
