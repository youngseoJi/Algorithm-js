## [algorithm/ 자료구조 큐 (Que) ] 공주를 구하러 갈 왕자 정하기

---

> 문제: N과 K가 주어질 때 공주를 구하러 갈 왕자의 번호를 출력해라!
> 왕자들이 N명이 있으며, 나이 순으로 1번부터 N번까지 차례로 번호를 매긴다. 
>
> 그리고 1번 왕자부터 N 번 왕자까지 순서대로 앉아서, 1번 왕자부터 n번 왕자까지 순서대로 1부터 번호를 한개씩 말한다.
> K(특정숫자)를 말한 왕자는 공주를 구하러 갈 수 없다. 제외된 왕자의 다음 왕자부터 다시 1부터 시작하여 번호를 한개씩 말한다. 

> 입력
>  N : 왕자의 수 
>  K : 특정 숫자 

## 접근방식
- queue 큐 자료구조 활용, 선입선출 특징 활용하기
=> 왕자의 번호를 순서대로 조회하며, 특정 숫자가 k가 3인경우? 3번쨰 순서인 왕자가 제외되는 것이다.
=> k-1 을 하며 특정숫자 직전까지 왕자를 맨 뒷 순서로 보내고, 그 다음 k번째인 왕자는 제거한다.
=> 반복하다보면 1명만 남을 것


## 풀이 
1. 왕자들을 순서대로 줄세울 que 변수를 선언 [] 을 할당한다.
2. for 문) 1번부터 n번 까지의 왕자까지 순서대로 담는다. (줄 세운다)
3. while 문) que의 길이가 1이 아닌 경우 반복, 길이가 1이되면 while문을 탈출한다.  => 왕자가 1명 남은 경우 탈출하게 설정
4. for 문) 왕자의 수가 1부터 k 특정 숫자보다 작을 떄까지만,
=> 배열의 맨 앞 요소를 shift() 빼서 que에 push() 담아준다.  => 특정 숫자 k번 왕자일 경우 shift() 제거한다.
5. while문 que.length ===1 인경우 while문을 탈출한다.
6. que에 마지막 남은 que[0] 왕자의 번호를 출력한다.

```js
function solution(n, k) {
	let answer;
    let que = [];
      for (let prince = 1; prince <= n; prince++) {
       que.push(prince);
       console.log(que);
      }
      while (que.length !== 1) {
     	for (let prince = 1; prince < k; prince++) {
    	  que.push(que.shift());
        }
         que.shift();
      }
      return que[0];
    }

      console.log(solution(8, 3));
```

### 선생님 코드와 내 코드와 다른 점
선생님은 queue 배열에 1부터 n까지의 수를 순서대로 담을때 Array.form() 메소드로 유사배열방식으로 담아줬다.
ex) [1,2,3,4,5,6,7,8]
```js
let queue = Array.from({length:n}, (v, i) => i+1)
// 길이는 n 까지의 배열을 만든다.
// v(value)와 i(index)를 전달받아서 i+1을 queue []에 담아준다.
// i+1인 이유는 왕자는 1번 부터기때문에 인덱스는 0부터니깐 1을 더해줘서 1부터 배열에 n길이만큼 담아주는 것
```

while문의 조건설정이 달랐고, 내부에 if문을 한번 더 사용해서 1일경우 따로 조건을 설정해주심
```js
while (queue.length) // if(que.length === 1) que.shift();
```
