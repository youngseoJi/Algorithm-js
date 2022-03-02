## [Algorithm/투포인터 알고리즘-1]  두 배열 합치기 (sort(), 투 포인터 알고리즘)

---

   > 문제 : 두배열 합치기 - 두 배열을 오름차순으로 합쳐라 

## 내 풀이 

  concat() -> 배열의 요소를 합쳐주는 메소드
       1. 두 배열을 concat() 을 사용해서 합쳐준다.
       2. 합친 배열을 sort() 로 오름차순 정려해준다.

​      

## 코드
```js

function solution(arr1, arr2) {
        let newArr = arr1.concat(arr2).sort((a, b) => a - b);
        // [1, 2, 3, 3, 5, 6, 7, 9]
      }

      let a = [1, 3, 5];
      let b = [2, 3, 6, 7, 9];
      console.log(solution(a, b));

```
 ## 선생님 접근방식 
### 기초) 투 포인터 알고리즘(Two Pointers Algorithm)
이름 그대로 두가지 포인트를 변수로 잡고 비교하는 알고리즘이다. - 더 복잡하지만 연습용!
이 알고리즘을 연습하라고 이 방식으로 하시는 것!

## 코드 (Two Pointers Algorithm)
```js
function solution2(arr1, arr2) {
        let answer = [];
        let len1 = arr1.length;
        let len2 = arr2.length;
        // p1,p2 = 인덱스 / 두개의 포인트 변수!
        let p1 = (p2 = 0); // 0번째 요소 부터 조회하기 위해 0을 할당

        // 둘중의 하나라도 거짓이면 거짓이 되므로 && 연산자사용

        // 배열의 인덱스가 배열길이랑 같거나 커지면?
        // -> 모든 배열을 다 조회한 것 -> while문을 멈춘다.
        while (p1 < len1 && p2 < len2) {
          // arr1의 요소가 arr2요소보다 작거나 같으면?
          if (arr1[p1] <= arr2[p2]) {
            // arr1[p1] p1 번째 인덱스 요소를 넣는다. -> 다음 인덱스 ++ 1을 증가(후치연산자)한다. (다음 요소 비교하기위해)
            answer.push(arr1[p1++]);
          } else {
            // arr2요소가 더 크면?
            // arr2[p2] p2 번째 인덱스 요소를 넣는다. ->  인덱스 ++ 1을 증가(후치연산자)한다.
            answer.push(arr2[p2++]);
          }
        }
        // 더 긴 배열의 나머지 요소들 담기
        // arr1[p1] 배열요소가 남았을 겨우 실행
        while (p1 < len1) {
          answer.push(arr1[p1++]);
        }
        // arr2[p2] 배열요소가 남았을 겨우 실행
        while (p2 < len2) {
          answer.push(arr1[p2++]);
        }
        return answer;
      }

      let a = [1, 3, 5];
      let b = [2, 3, 6, 7, 9];
      console.log(solution2(a, b));
```