## [algorithm] JS - 짝을 만들 수 있는 경우의 수(이중배열, 이중for문)



> 문제 : M번의 테스트 등수로 멘토와 멘티 짝을 만들 수 있는 경우의 수를 구해라
> 멘토는 멘티보다 M번의 수학테스트에서 모두 등수가 높아야한다.

- 입력 : 반 핵생수 (1 <= n <= 20), 수학 테스트 횟수 M (1<= M <= 10)
  
  test[테스트 횟수][몇번째 학생] = test[m][n]
    M : test[0], test[1], test[2]...
    N : test[0][1],  test[0][2],  test[0][3],  test[0][4]....
      let test = [
        [3, 4, 1, 2], -> 학생수 n = test[0].length = 4명
        [4, 3, 2, 1], 
        [3, 1, 4, 2],
        ];
       -> 총 테스트 횟수 m = test.length = 3번

### 풀이
1. 멘토와 멘티가 짝이될 경우의 수를 담을 변수 match 선언하고 초기 값 0할당한다.

2. 이중배열, m 수학테스트의 횟수는 배열의 길이를 담고, n 학생의 수에는 test 배열의 0번째 길이를 담는다.
    -> 총 학생 수 n = test[0].length = n명 / 총 테스트 횟수 m = test.length = m번
 3. 멘토 멘티가 되는 모든 경우의 수를 구하기 위해서 이중 포문으로 이중배열의 모든 요소를 조회한다.
      -> i = 멘티, j = 멘토로 정하고 생각하기!
    -> 총 학생수가 만약 4명이면 16가지의 경우의 수가 나온다.
4. 그 다음 멘티와 멘토의 각 등수를 조회하기 위해, 이중 포문으로 이중배열의 모든 요소를 조회 비교한다.
    -> 1번 포문) 수학테스트 횟수 m 직전 까지 2번포문) 등수가 학생 수 만큼까지 반복해서 조회해서 0번째 테스트의 1번째 학생이 i멘티 멘티르 담을 변수 menti에 = 등수를 담고 멘토를 담을 변수 mento에 해당 등수를 담는다.
5. pi < pj 해당 행 k번째 테스트에서 멘토가 멘티 등수보다 더 클 경우 
-> count ++ 에 1을 더해서 경우의 수를 올린다.
6. 모든 수학테스트동안 멘토가 멘티보다 큰 경우만 거르는 조건식 
   -> 멘토가 멘티보다 큰 경우의 수가 m 수학 테스트의 횟수와 같아야 match ++ 1을 더해준다.

   ```js
      function solution(test) {
        let match = 0;
        m = test.length;
        n = test[0].length;
        // 학생 수만큰 멘코멘티가 될 수 있는 모든 경우의 수 짝 구하는 식
        for (let i = 1; i <= n; i++) {
          for (let j = 1; j <= n; j++) {
            console.log(i,j)
            let cnt = 0;
            // 해당 행의 수학테스트에서 멘토와 멘티
            // 수학 테스트 횟수 m 직전 까지 (인덱스 0,1,2,3 이니깐 학생조회할때)
            for (let k = 0; k < m; k++) {
              let pi,pj = 0;
              // 등수 s 학생 수 만쿰
              for (let s = 0; s < n; s++) {
                // k번째 테스트의 s등수에 해당하는 i번째 학생
                if (test[k][s] === i) pi = s;
                // k번째 테스트의 s등수에 해당하는 j번째 학생
                if (test[k][s] === j) pj = s;
              }
              if (pi < pj) cnt++;
            }
            //  모든 수학테스트동안 멘토가 멘티보다 큰 경우만 거르는 조건식
            if (cnt === m) match++;
            // 멘토가 멘티보다 큰 경우의 수가 m 수학 테스트의 횟수와 같아야 match ++ 1을 더해준다.
          }
        }
        return match;
      }
   
      let arr = [
        [3, 4, 1, 2],
        [4, 3, 2, 1],
        [3, 1, 4, 2],
      ];
      console.log(solution(arr));