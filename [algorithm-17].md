## [algorithm/ 자료구조 스택 (stack) ] 크레인 인형뽑기, 터뜨린 인형의 개수

---

> 문제 : 인형뽑기 기계, 게임 화면의 격자의 상태가 담긴 2차원 배열 board와 인형을 집기 위해 크레인을 작동시킨 위치가 담긴 배열 moves가 매개변수로 주어질 때, 크레인 인형뽑기를 모두 작동시킨 후 터트려져 사라진 인형의 개수를 출력해라

>
>조건 1) 같은 인형이 두개를 연속으로 뽑으면, 두 인형이 사라진다.
>조건 2) board 배열은 2차원 배열로 크기는 5 x 5 이상 30 x 30 이하입니다.
>조건 3) board의 각 칸에는 0 이상 100 이하인 정수가 담겨있다.
>조건 4) 0은 빈 칸을 나타낸다.
>조건 5) 1 ~ 100의 각 숫자는 각기 다른 인형의 모양을 의미, (즉, 같은 숫자는 같은 모양의 인형)
>조건 6) moves 배열의 크기는 1 이상 1,000 이하
>조건 7) moves 배열 각 원소들의 값은 1 이상이며 board 배열의 가로 크기 이하인 자연수

## 접근방식
- **stack 스택 자료구조 후입선출특징활용)** 아래부터 차곡차곡 쌓여있는 인형들 중 맨 위의 인형부터 뽑을 수 있다. 
      => 뽑은 인형은 stack []에 뽑은 순으로 담아주며, 같은 인형을 연속으로 뽑았을 경우 제거한다.
      - 인형뽑기는 판은 board[행][열] 2차원 배열로 구성되어있다. 
      => 행과 열번호 해당 인덱스 활용하기
      => 열번호 === moves 배열(뽑기 위치), 즉  board[행][열] 열번호(배열길이)이다. length-1해서 = 열번호 index로 배열 탐색가능

## 풀이

1. 변수 stack 선언, 뽑은 인형을 순서대로 담을 바구니, 빈배열 [] 할당한다.

2. 이중 for문) 5 * 5 board 2차원 배열을 조회하기 위해 이중 포문으로 숫자 요소(각 인형)를 조회한다.
3. 외부 for) 인형을 뽑을 위치가 담긴 moves 배열의 수 요소(board의 열 길이)를 모두 조회한다.
4. 내부 for) moves 배열요소, 즉 board의 열을 1번 조회할때 board의 행 길이까지를 돌며 행 요소를 조회한다. 
= > 열고정 , 내부 포문 행의 요소를 다 조회한 후 => 다음 열을 조회하는 식 
5. 내부 for문 내 if조건문
6. if문) 뽑은 인형(보드의 행열 요소)가 0이 아닌 경우, (인형이 있는 2차원 배열 요소)
7. while문) 뽑으려는 인형(보드 행열 요소)과 같은 인형이 바구니에 맨위(stack의 마지막요소)에 담겨있는 경우? 
=> 뽑은 인형이 있던 보드의[헹][열-1]요소를 0으로 변경한다. 뽑았으니 인형이 없는 것이니깐!
=> stack.pop() 으로 stack의 맨 위 인형을 삭제한다. (뽑은 인형과 같은 인형)
=> cnt 개수를 인형이 2개 제거되었으니 +2 올려준다.
8. while문 탈출조건) 뽑는 인형과 stack 바구니에 담긴 맨위 인형과 다를 경우?
=>  while문을 종료하고 뽑은 인형을 stack바구니에 담는다.
9. 2차원 배열을 조회하는 for문이 종료되고, 인형이 몇개 제거되었는지 cnt를 리턴한다.


```js
function solution(board, moves) {
    let cnt = 0;
    let stack = [];
      // 열 조회
    for (let column = 0; column < moves.length; column++) {
        // 행 조회 (1열 조회 후 모든 행 조회식)
      for (let row = 0; row < board.length; row++) {
          //
        if (board[row][column - 1] !== 0) {
          while (board[row][column - 1] === stack[stack.length - 1]) {
            board[row][column - 1] = 0;
            stack.pop();
              cnt += 2;
            }
            // 같지 않은경우 stack에 뽑은 인형을 담는다.
            stack.push(board[row][column - 1]);
          }
        }
      }
      return cnt; // 4
    }

      let board = [
        [0, 0, 0, 0, 0],
        [0, 0, 1, 0, 3],
        [0, 2, 5, 0, 1],
        [4, 2, 4, 4, 2],
        [3, 5, 1, 3, 1],
      ];

      let moves = [1, 5, 3, 5, 1, 2, 1, 4];
      console.log(solution(board, moves));
```



### 선생님 코드와 내 코드의 다른 점

선생님은 이중for문과 while문을 사용하시지 않았다.
forEach문으로 반복문이 한바퀴 돌때 고정되는 행번호를 조회하고, 열번호만 for문으로 조회했다. while문으로 추가적인 반복문을 사용하지 않고, if문으로 조건을 더 나누시고, break문을 사용하여 stack []에 인형 개수를 담은 후 현재 행의 조회를 멈추고, 다음 행으로 넘어가 해당 행의 열번호(요소)를 조회한다.
```js
moves.forEach(pos => {
 for (let row = 0; i < board.length; i++) {
    if (board[i][pos-1] !== 0) {
      let tmp = board[i][pos-1];
       board[i][pos-1] = 0;
      if (tmp === stack[stack.length - 1]) {
        stack.pop();
        answer += 2;
   	  }
      	else stack.push(tmp)
      	break;
   		}
 	  }
	});
	return answer;
}
```
