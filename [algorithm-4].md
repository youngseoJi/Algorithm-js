## [Algorithm] - 문자열에서 숫자문자만 추출하기 (isNaN() 매개변수 숫자로 강제변환)

---



>**문제 : 문자열내에서 숫자만 추출하여, 해당 문자숫자를 순서대로 자연수로 만든다.**

> 새로배운 점 : isNaN()는 매개변수를 숫자로 강제 변환시킨다!! 

## 풀이

1.입력되는 문자열내에서 문자타입인 숫자만 추출하여, 해당 문자숫자를 순서대로 자연수로 만든다.

2. 문자열의 각 문자를 모두 조회해서 숫자타입을 거른다. -> !isNaN()
3. 숫자만 담긴 배열을 문자열로 변환하고 수로 변환한다. -> Number()

```js
function solution(str) {
  let num = "";
   for (let i of str) {
   // isNaN 은 업격하지 않은 비교여서 매개변수를 숫자로 변환시킨다.
     if (!isNaN(i)) {
         num += i;
     }
   }
   return Number(num);
 }

 let str = "1ys2coding666";
 console.log(solution(str));  // -> 12666
```