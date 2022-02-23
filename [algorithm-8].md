## [Algorithm] JS - 소수 판별하기,  요소 뒤집기 (Math.sqrt(), reverse())

> 문제 : 자연수를 뒤집은 후 그 뒤집은 수가 소수이면 그 소수를 출력
>    예외) 첫 자리의 0을 무시한다. 012 -> 12 , 0012 0-> 12

>[소수](https://namu.wiki/w/%EC%86%8C%EC%88%98(%EC%88%98%EB%A1%A0))
>1, -1과 자기 자신, 자기 자신의 반수[1]로밖에 나누어떨어지지 않는 1 이외의 정수로, 즉 양의 약수가 단 두 개뿐인 수를 의미한다.
>소수의 정의는 '1과 자기 자신으로밖에 나누어 떨어지지 않고 자기 자신의 곱셈의 역수가 없는 수'이다.


### 소수 판별하는 2가지 방법
공통 1은 소수가 아니므로 제외하고 시작하며, 2부터 소수는 시작!
- **절반까지만 판별하기 num/2**
 해당 수의 절반까지만 돌려서 자기자신이 아닌 수로 나누어 떨어지면 소수가 아니다. (소수점은 parseInt())
  절반이 넘어가면 어짜피 같은 방식을 반복하는 것


```js
 num = 16일때 약수는 1 * 16, 2 * 8, 8 * 2 다.  -> 8*2 를 또 확인할 필요없다.
```
- **제곱근 까지만 판별하기 Math.sqrt(num)**
  즉 루트를 씌운값 까지만 판별하는 것,√N  각 약수에 루트를 씌우면 거의 중간값이 나온다. (소수점은 parseInt())
****



### 풀이
1. 배열의 각 자연수 요소를 뒤집어 주기 위해 배열의 모든 요소를 조회한다.
2. 각 숫자타입의 요소를 뒤집어 주기위해서 toString()으로 문자열로 변형, 변형된 각 요소를split("')으로 쪼개 나눠준다. 
3. reverse로 각 요소의 순서를 뒤집고, join("")으로 요소를 다시 합해준 다음 number()로 숫자타입으로 변형한다.
-> 각 요소에 메소드를 사용하는 모습 ! ![](https://images.velog.io/images/estell/post/fec8cd78-66c2-4538-9d7c-0c665f89f723/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-02-13%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%204.31.32.png)
4. 소수로 변환시키는 부분은 따로 함수를 생성한다! 
5. 1과 자기사진으로만 나누어지는 특성을 생각하여 1인경우에는 예외처리 false!
6. 2부터 num을 2로 나눈 수 또는 제곱근까지만 조회하여, 자기 자신이 아닌 수로 각 요소가 0으로 떨어지는 경우 약수가 아니다. false !
7. isPrime(num) 소수판별함수를 사용하여 if() 소수일경우에만 빈 배열 Result에 담아 소수만 담긴 배열을 출력한다.


 ```js
 function isPrime(num) {
        if (num === 1) return false;
   		if (num === 2) return true;
        
        //for (let i = 2; i <= parseInt(i<=num/2); i=i+2) {
        for (let i = 2; i <= parseInt(Math.sqrt(num)); i++) {
          if (num % i === 0) return false;
        }
        return true;
      }
      function solution(arr) {
        let result = [];
        for (let el of arr) {
          let reverseNum = Number(el.toString().split("").reverse().join(""));
          // [23, 55, 26, 2, 52, 73, 2, 3, 1]
          if (isPrime(reverseNum)) {
            result.push(reverseNum);
          }
        }
        return result; //  [23, 2, 73, 2, 3]
      }

      let arr = [32, 55, 62, 20, 250, 370, 200, 30, 100];
      console.log(solution(arr));