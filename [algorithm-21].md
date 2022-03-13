## [algorithm/ 버블정렬 ] 오름차순으로 정렬하기(or 조건에 맞게 정렬)

---

> 문제 : N개이 숫자가 입력되면 오름차순으로 정렬하여 출력해라

> 조건1) 버블정렬으로 정렬 (sort말고)

## 접근방식 - 버블정렬
- 버블정렬? 서로 인접한 두 원소를 검사하여 정렬하는 알고리즘, 인접한 2개의 레코드를 비교하여 크기가 순서대로 되어 있지 않으면 서로 교환한다.
      => 시간복잡도가 최악이라 거의 안쓰는 방법이다. 
      [버블정렬 정리 잘해놓은 블로그](https://gmlwjd9405.github.io/2018/05/06/algorithm-bubble-sort.html)
- 오름차순 정렬을 한다면, 이중 for으로 앞뒤요소를 비교하고 
      => 앞의 요소가 크면 그 다음 요소와 자리교체, 
      => 앞에 요소가 작으면 그 다음 요소와 교체하지 않고 다음 요소들을 비교한다. 
      => 이때 요소의 개수-1 번만큼 계속 돌며 비교와 교체를 반복해주고 이중 for문이 종료되면 정렬되어있는 것이다.
      
## 풀이
1. 이중 for문을 사용한다. (앞의 요소와 그 다음 요소를 비교하기 위해 조회한다.) 

2. 외부 for문) i=0번째 요소부터 마지막 요소 arr.length-1 전 요소 만큼 내부 j for문 반복힌다. 
3. 내부 for문) j=0 번째 요소부터 arr.length-i-1번째 요소까지 조회한다.
=> arr.length-i-1번째 요소까지인 이유는? 
=> 이미 비교 교체가 완료된 요소들를 또 비교정렬할 필요없어서 i번째 회전을 할때 마다 비교하는 j번째 요소개수도 줄어드는 것
4. i번째 요소 j번 부터 j< arr.length-i-1번째 요소까지 다 비교하여 
4-1. if문) j가 j+1보다 더 클 경우?
=> j와 j의 위치를 변경한다.
4-2. if문) j가 j+1보다 작은 경우? 
=> j와 j+1의 위치를 변경하지 않는다. => continue
5. j와 모든 j+1를 비교했으면, j=1 부터 다음 요소 j+1을 비교 교체하기를 반복힌다.
6. i for문 이 종료되면 반복문을 탈출하고 오름차순으로 정렬된 배열을 출력한다.
```js
	function solution(arr) {
        for (let i = 0; i < arr.length - 1; i++) {
          for (let j = 0; j < arr.length - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
              [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
            } else {
              continue;
            }
          }
        }
        return arr;
      }

      let arr = [13, 5, 11, 7, 23, 15];
      console.log(solution(arr));
```

## 위 문제와 다른 부분
- 앞의 요소가 양수이고 다음 요소가 음수인 경우?
=> 요소의 위치를 서로 바꿔줍니다.

```js
 if (arr[j] > 0 && arr[j + 1] < 0) {
	[arr[j], arr[j + 1]] = [arr[j + 1], arr[j]]
 };
```

```js
function solution(arr) {
        for (let i = 0; i < arr.length - 1; i++) {
          for (let j = 0; j < arr.length - i - 1; j++) {
            if (arr[j] > 0 && arr[j + 1] < 0) {
              [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
            }
          }
        }
        return arr;
      }

      let arr = [1, 2, 3, -3, -2, 5, 6, -6];
      console.log(solution(arr));
