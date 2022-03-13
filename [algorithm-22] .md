## [algorithm/ 삽입정렬 ] N개의 숫자를 오름차순 정렬하기

---

> 문제 : 삽입정렬로 N개의 숫자를 오름차순 정렬하기

## 접근방식 - 삽입정렬
- 삽입정렬 : 두 번째 자료부터 조회를 시작하여 그 앞(왼쪽)의 자료들과 비교하여 삽입할 위치를 지정한 후 자료를 뒤로 옮기고 지정한 자리에 자료를 삽입하여 정렬하는 알고리즘
=> 2번째 요소와 1번째 요소를 비교, 3번째 요소와 2번째, 1번째 요소를 비교하며 삽입할 요소의 위치를 찾으면 
=> 해당 요소를 삽입하기 위해 요소들을 뒤로 밀어서 만든 사이에 삽입하는 것이다.

[삽입정렬 정리잘 된 블로그](https://gmlwjd9405.github.io/2018/05/06/algorithm-insertion-sort.html)

## 풀이

1. i 외부 for 문) i= 1번째 요소부터(2번째) arr.length마지막 요소까지 조회한다.

2. j 내부 for 문) j= i번째 요소 부터 j>=0 때까지 j-1을 하며, 맨 앞의 요소 0번째 요소까지 조회한다.
2-1. if 문) arr[j-1]가 arr[j] 보다 큰 경우?
=> 1번째 요소가 2번째 요소보다 큰 경우 정렬하기 위해, 두 수의 위치를 교체해준다.
=> arr[j]에 arr[j-1] 값을 담아주고, arr[j-1]에 arr[j] 값을 담아준다. 
2-2. else 문) arr[j-1]가 arr[j]보다 작은 경우?
=> break!
3. 다시 i=2 부터 반복 시작! 반복문이 완전히 종료되면 정렬된 배열을 출력한다.
```js
      function solution(arr) {
        for (let i = 1; i < arr.length; i++) {
          for (let j = i; j >= 0; j--) {
            if (arr[j - 1] > arr[j])
              [arr[j], arr[j - 1]] = [arr[j - 1], arr[j]];
            else break;
          }
        }

        return arr;
      }

      let arr = [11, 7, 5, 6, 10, 9];
      console.log(solution(arr));
```
## 선생님 풀이

```js
      function solution2(arr) {
        for (let i = 1; i < arr.length; i++) {
          // 임시변수에 arr[i]값을 복사해서 담아 사용한다.
          let tmp = arr[i],
          j;
          // 스코프 범위 떄문에 j를 외부 포문에서 변수를생성해준다.
          for (j = i - 1; j >= 0; j--) {
            // 앞의 요소가 뒤의 요소보다 클 경우?
            if (arr[j] > tmp) {
              // 뒤 요소에 앞의 요소를 담아준다.
              arr[j + 1] = arr[j]; // 한칸씩 뒤로 밀어주는 작업 삽입할 자리 만들기
            }
            // 앞의 요소가 뒤의 요소보다 작을 경우?
            else break;
          }
          // 반복문 종료 후 요소 삽입하기
          arr[j + 1] = tmp;
        }
        return arr;
      }

      let arr = [11, 7, 5, 6, 10, 9];
      console.log(solution2(arr));
```
