# Chapter 2 
- 배열

##### 2.1 자바스크립트 배열 정의
- 배열은 정수 인덱스 (오프셋) 을 이용해 각 요소에 접근할 수 있게 순차적으로 요소를 저장한 집합체이다.
- 프로그래밍 언어 대부분은 배열을 제공한다.
- 하지만 자바스크립트는 일반적인 프로그래밍 언어와는 다른 종류의 배열을 제공한다.

- 자바스크립트의 배열은 특화된 자바스크립트 객체이며, 정수 인덱스로 객체 내의 데이터 오프셋을 표현한다.
- 정수를 인덱스로 사용하면 자바스크립트 객체 요구사항에 맞게 `내부적으로 정수를 문자열로 변환한다.`

- 자바스크립트 배열은 자바스크립트 객체지만, 내부적으로는 특화된 객체 이므로 배열로 취급한다.



##### 2.2 배열 사용하기
- 자바스크립트의 배열은 매우 유연하다.
- 배열을 생성하고, 접근및 저장된 요소를 검색하거나 정렬하는 등의 동작을 다양한 방법으로 수행할 수 있다.



##### 2.2.1 배열 만들기
- 배열을 선언하는 방법은 크게 두가지로 나뉜다.

- 1) 기본적인 배열 선언 방법
    - 1. [] 기호만 선언 하는 방법
        - 길이가 0인 배열이 생성된다.
    - 2. [] 기호안에 요소 집합을 이용해 생성하는 방법
        - 해당 요소 집합을 가지는 배열이 생성된다.    
    - length 속성을 활용하여 배열의 길이를 확인할 수 있다.
    
```javascript
// 길이가 0인 배열을 생성하는 방법
var numbers = [];
print(numbers.length);

// 요소 집합을 이용해 배열을 생성하는 방법
var numbers = [1, 2, 3, 4, 5];
print(numbers.length); // 5 출력
```


- 2) Array 생성자를 활용한 배열 선언 방법
    - 1. 아무런 인자를 가지지 않는 생성자를 활용한 방법 
        - 길이가 0인 배열이 생성된다.
    - 2. 생성자의 인자에 요소 집합을 제공하는 방법
        - 해당 요소 집합을 가지는 배열이 생성된다.
    - 3. 생성자에 배열의 길이를 지정하는 한 개의 인자를 제공하는 방법
        - 해당 인자의 값 만큼 길이가 지정된다.
        
```javascript
// 길이가 0인 배열을 생성하는 방법
var numbers = new Array();
print(numbers.length); // 0 출력

// 요소 집합을 이용해 배열을 생성하는 방법
var numbers = new Array(1, 2, 3, 4, 5);
print(numbers.length);

// 배열의 길이를 지정하는 한 개의 인자를 제공하는 방법
var numbers = new Array(10);
print(numbers.length); // 10 출력
```

- Array.isArray()
    - 특정 객체가 배열인지 확인하는 함수
```javascript
var numbers = 3;
var arr = [7, 4, 1776];
print(Array.isArray(numbers)); // false 출력
print(Array.isArray(arr)); // true 출력
```   

- 자바스크립트의 배열
    - 다른 언어와 달리 자바스크립트에서는 한 배열이 다양한 타입의 요소를 포함할 수 있다. 
        - 대부분의 스크립트 언어의 특성
    - 다양한 방법으로 배열을 생성할 수 있지만 Array 생성자 호출보다는 [] 기호를 사용하는것이 더 효율적이라고 추천한다.    



##### 2.2.2 배열 요소 접근 및 값 변경하기
- 배열 요소의 값 할당 방법
    - 할당 문에 [] 를 이용하여 배열 요소에 값을 할당할 수 있다.
```javascript
var numbers = [];
for (var i = 0; i < 100; i++) {
    numbers[i] = i+1;
}
```

- 배열 요소의 접근 방법
    - [] 를 이용하여 배열의 요소에 접근할 수 있다.
    - 반복문을 사용하여 순차적인 접근이 가능하다.
```javascript
// [] 을 이용하여 배열의 요소에 접근하는 방법
var numbers = [1, 2, 3, 4, 5];
var sum = numbers[0] + numbers[1] + numbers[2] + numbers[3] + numbers[4];
print(sum); // 15 출력

// 반복문을 사용하여 배열의 요소에 순차적으로 접근하는 방법
var numbers [1, 2, 3, 4, 5];
var sum = 0;
var length = numbers.length;
for (var i = 0; i < length; i++) {
    sum += numbers[i];
}
```

- 반복문 사용시 주의점
    - 보통 for문 안에 length를 사용하는데 갯수가 작을때는 차이가 미미하다.
    - 하지만 갯수가 많아 질수록 성능 차이가 난다.
    - for문 안에서 length 사용시 루프 돌때마다 계산을 해야하기때문에 속도가 많이 걸린다.
    

##### 2.2.3 문자열로 배열 생성하기
- 문자열의 split() 함수를 호출하면 배열이 생성된다.
- split() 함수는 문자열을 특정 구분자로 분리한 다음 분리된 문자열을 포함하는 배열을 만든다.

```javascript
var sentence = 'javascript html css';
var words = sentence.split(' ');
var length = words.length;
for (var i = 0; i < length; i++) {
    print(`${i}번째 단어 = words${i}`);
}
// 출력결과
/*
0 번째 단어 = javascript
1 번째 단어 = html
2 번째 단어 = css
*/
```

  
##### 2.2.4 배열 전체에 적용되는 기능
- 배열을 다른 배열로 할당하기
    - 대입연산자 (=) 를 사용하여 기존 배열을 다른 변수에 할당할 수 있다.
        - 기존 배열의 주소(레퍼런스)를 할당하는것이다.
        - 원본 배열을 변경하면 할당된 배열도 변경된다.
```javascript
var numbers = [];
for (var i = 0; i < 10; i++) {
    numbers[i] = i + 1;
}
var sameNumbers = numbers; // sameNumbers에 numbers 배열을 할당
```


- 얕은복사 (Shallow Copy)
    - 대입연산자를 사용하여 배열을 할당할 경우 주소를 할당하는 것이다.
    - 할당된 배열은 원본 배열을 가리키고 있을 뿐이다.
    - 원본 배열을 변경하면 할당된 배열도 변경되는데 이를 얕은복사 (Shallow Copy) 라고 한다.
```javascript
var numbers = [];
for (var i = 0; i < 10; i++) {
    numbers[i] = i + 1;
}
var sameNumbers = numbers; // sameNumbers에 numbers 배열을 할당
numbers[0] = 400; // 원본 배열인 numbers의 값을 변경
print(sameNumbers[0]); // 400 출력
```

`얕은 복사 보다 깊은 복사 (Deep Copy) , 원래 배열 요소를 새로운 배열 요소로 복사하는 기능이 필요할 때가 있다.`

- arr1 배열의 요소를 arr2로 깊은복사 (Deep Copy) 하는 함수
```javascript
function copy (arr1, arr2) {
    var length = arr1.length;
    for (var i = 0; i < length; i++) {
        arr2[i] = arr[1];
    }  
}
```

- 깊은 복사(Deep Copy)
    - 원본 배열을 가리키는 것이 아닌 원본 배열의 요소의 값을 새로운 배열 요소의 값으로 복사한다.
    - 원본 배열이 수정되어도 복사된 배열에 영향을 미치지 않는다.
```javascript
var numbers = [];
for (var i = 0; i < 100; i++) {
    numbers[i] = i + 1;
}
// numbers [0, 1, 2, 3 ... 100]
var sameNumbers = [];
copy(numbers, sameNumbers);
// copy 이후 
// numbers [0, 1, 2, 3 ... 100] / sameNumbers [0, 1, 2, 3 ... 100]
numbers[0] = 400; // numbers [400, 1, 2, 3 ... 100] / sameNumbers [0, 1, 2, 3 ... 100]
print(sameNumbers[0]); // 원본 배열이 400 으로 수정되었으나 Deep Copy 되었기 때문에 1 출력
```

- print() 함수
    - 배열의 내용을 출력 한다.
```javascript
var numbers = [1, 2, 3, 4, 5];
print(numbers); // 1,2,3,4,5
```


#### 2.3 접근자 함수
- 자바스크립트는 배열 요소에 접근 가능한 다양한 함수를 제공한다.
- 이를 접근자 함수 (Access Function) 이라 부르며 특정값을 포함하는 결과 배열을 반환한다.


##### 2.3.1. 검색
- IndexOf()
    - 인자로 제공된 값이 배열에 존재하는지 여부를 알려준다.
        - 존재한다면 양수
        - 값이 없다면 -1을 반환한다.
    - 찾고자 하는 값이 배열에 여러개 존재한다면 첫 번째로 발견한 인덱스를 반환한다.
    
```javascript
var names = ['정곰', '혜지몽', '흑곰'];
printstr('찾고 싶은 이름을 입력히세요');
var name = readLine();
var position = names.indexOf(name);
if (position > 0) {
    print(`${name} 을 찾았습니다. 위치는 ${position} 입니다.`);
} else {
    print(`${name} 은 배열에 존재하지 않습니다.`);
}
```

- lastIndexOf()
    - indexOf() 함수와 비슷한 함수
    - 배열에서 일치하는 값중 마지막 인자의 위치를 반환한다.
        - 존재한다면 양수
        - 값이 없다면 -1을 반환한다.

```javascript
var names = ['정곰', '혜지몽', '흑곰'];
printstr('찾고 싶은 이름을 입력히세요');
var name = readLine();
var position = names.lastIndexOf(name);
if (position > 0) {
    print(`${name} 을 찾았습니다. 위치는 ${position} 입니다.`);
} else {
    print(`${name} 은 배열에 존재하지 않습니다.`);
}
```

##### 2.3.2 배열을 문자열로 표현하기
- join()
    - 배열을 문자열 형식으로 반환하는 함수
    - 배열의 요소를 인자로 받은 구분자로 구분하는 문자열을 반환한다.
```javascript
var names = ['정곰', '혜지몽', '흑곰'];
var nameStr = names.join();
print(nameStr);
```

- toString
   - 배열을 문자열 형식으로 반환하는 함수
   - print() 함수의 인자로 배열의 이름을 제공하면 자동으로 배열의 toString() 함수가 호출된다.
```javascript
var names = ['정곰', '혜지몽', '흑곰'];
print(names); // 정곰,혜지몽,흑곰
```   

##### 2.3.3 기존 배열을 이용해 새 배열 만들기
- concat()
    - 기존 배열을 이용해 새 배열을 만드는 함수이다.
    - 두 개 이상의 배열을 합쳐 새 배열을 만든다.
        - 기존 배열에 concat() 함수를 호출하면 인자로 다른 배열을 제공한다.
        - 인자로 제공된 배열이 concat() 함수를 호출한 배열의 뒤로 추가된다.
```javascript
var bears = ['정곰', '흑곰'];
var mongs = ['혜지몽', '곰탱몽'];
var concatedArr = bears.concat(mongs);
print(concatedArr); // 정곰,흑곰,혜지몽,곰탱몽
```

- splice()
    - 기존 배열을 이용해 새 배열을 만드는 함수이다.
    - 기존 배열의 서브셋으로 새 배열을 만든다.
        - 사용할 첫 요소의 위치, 사용할 요소의 수를 인자로 받는다.
    - 배열에 요소를 추가하거나 제거하는 등 배열을 고치는 용도로 활용할 수 있다.
```javascript
var bears = ['정곰', '흑곰', '혜지곰', '월평동흑곰'];
var splicedArr = bears.splice(0, 2);
print(splicedArr); // 정곰, 흑곰
```


#### 2.4 변형자 함수
- 개별적으로 요소를 건드리지 않고 배열 전체 내용을 고치는 변형자 함수 (Mutator Function) 을 제공한다.


##### 2.4.1 배열에 요소 추가하기
- push()
    - 배열의 끝에 요소를 추가한다.
    - length property를 이용해 배열을 확장하는것 보다 push() 함수를 사용하는것이 더 직관적이다.
```javascript
var nums = [1, 2, 3, 4, 5];
print(nums); // 1, 2, 3, 4, 5
nums.push(6);
print(nums); // 1, 2, 3, 4, 5, 6
```

- unshift()
    - 배열의 맨 앞에 요소를 추가한다.
```javascript
var nums = [2, 3, 4, 5];
print(nums); // 2, 3, 4, 5
nums.unshift(1);
print(nums); // 1, 2, 3, 4, 5
```



##### 2.4.2 배열의 요소 삭제하기
- pop()
    - 배열의 마지막 요소를 제거한다.
    - 제거된 요소를 반환한다.
```javascript
var nums = [1, 2, 3, 4, 5, 9];
nums.pop();
print(nums); // 1, 2, 3, 4, 5
```

- shift()
    - 배열의 맨 앞 요소를 제거한다.
    - 제거된 요소를 반환한다.
```javascript
var nums = [9, 1, 2, 3, 4, 5];
nums.shift();
print(nums); // 1, 2, 3, 4, 5
```


##### 2.4.3 배열 중간에 요소를 추가하거나 삭제하기
- 배열 중간에 요소를 추가하거나 삭제할때도 다른 요소를 이동시켜야 하는 문제가 생긴다.
- splice() 함수를 이용하면 한번에 두 가지 동작을 수행할 수 있다.

- splice()
    - 배열에 요소를 추가하려면 세가지 인자가 필요하다.
        - 시작 인덱스 (어느 지점부터 추가할 것인가)
        - 삭제할 요소의 개수 (요소 추가시에는 0)
        - 배열에 추가할 요소들
```javascript
// 배열에 요소 추가하기
var nums = [1, 2, 3, 7, 8, 9];
var newNums = [4, 5, 6];
nums.splice(3, 0, 4, 5, 6);
print(nums); // 1, 2, 3, 4, 5, 6, 7, 8, 9

// 배열의 요소 삭제하기
var nums = [1, 2, 3, 4, 5, 100 ,200 ,300];
nums.splice(5, 3);
print(nums); // 1, 2, 3, 4, 5
```

* splice(3, 0, newNums); 를 하지않는 이유 ?
- 배열을 추가하는것이 아닌 요소를 추가하기 때문에 splice(3, 0, newNums); 로 함수를 호출하게 되면 결과는 다음과 같다.
```javascript
// 1, 2, 3, [4, 5, 6], 7, 8, 9
```

##### 2.4.4 배열 요소 정렬하기
- reverse()
    - 배열의 요소를 역순으로 바꾼다.
```javascript
var nums = [1, 2, 3, 4, 5];
nums.reverse();
print(nums); // 5, 4, 3, 2, 1
```

- sort()
    - 배열의 요소를 순서대로 정렬한다.
    - 문자열을 정렬할때 유용하다.
    - 숫자는 생각한대로 정렬되지 않는다.
    - 배열의 요소를 모두 문자열로 간주하고 알파벳 순으로 요소를 정렬한다.
    - 순서를 결정해주는 함수를 전달하면 해당 함수를 이용해 정렬을 진행한다.
```javascript
// 문자열 정렬
var names = ['Bravo', 'Ayo', 'Mike'];
names.sort();
print(names); // Ayo, Bravo, Mike

// 숫자 정렬
var nums = [200, 1, 3, 5, 8 ,400];
nums.sort();
print(nums); // 1, 200, 3, 400, 5, 8

// 정렬 함수 제공
var nums = [200, 1, 3, 5, 8, 400];
nums.sort((num1, num2) => num1 - num2);
print(nums); // 1, 3, 5, 8, 200, 400
```

#### 2.5 반복자 함수
- 반복자 함수는 배열의 각 요소에 함수를 적용한 뒤 그 결과 값 또는 값의 집합 또는 새로운 배열을 반환한다.


##### 2.5.1 배열을 만들지 않는 반복자 함수
- 배열을 만들지 않고 각 요소에 어떤 작업을 수행하거나 배열에 어떤 작업을 수행한 다음 한 개의 값을 생성하는 함수이다.

- forEach()
    - 배열을 만들지 않는 반복자 함수
    - 배열의 모든 요소에 인자로 받은 함수를 호출한다.
```javascript
function square (num) {
    print(num, num * num);
}

var nums = [1, 2, 3, 4, 5];
nums.forEach(square);
/*
출력 결과
1 1
2 4
3 9
4 16
5 25
*/
```

- every()
    - 배열을 만들지 않는 반복자 함수
    - boolean 함수를 배열에 적용해 배열의 모든 요소가 참이라면 true를 반환한다.
```javascript
function isEven (num) {
    return num % 2 === 0;
}

var nums = [2, 4, 6, 8, 10];
var even = nums.every(isEven);
if (even) {
    print('모든 수가 짝수 입니다.');
} else {
    print('모든 수가 홀수 입니다.');
}
// 출력결과
// 모든 수가 짝수 입니다.
```

- some()
    - 배열을 만들지 않는 반복자 함수
    - 배열 요소 중 한 요소라도 기준을 만족한다면 true를 반환한다.
```javascript
function isEven (num) {
    return num % 2 === 0;
}

var nums = [1, 2, 5, 7, 8, 13];
var even = nums.some(isEven);
if (even) {
    print('짝수인 수가 존재합니다.');
} else {
    print('짝수인 수가 존재하지 않습니다.');
}
// 출력 결과
// 짝수인 수가 존재합니다.
```

- reduce()
    - 배열을 만들지 않는 반복자 함수
    - 누적자 함수를 인자로 받은 뒤 배열의 모든 요소를 누적자 함수에 적용한다.
```javascript
function add (total, currentValue) {
    return total + currentValue;
}
var nums = [1, 2, 3, 4, 5];
var sum = nums.reduce(add);
print(sum); // 15
```
    
- reduceRight()
    - reduce() 함수와 같은 동작을 수행한다.
    - 배열의 오른쪽 요소에서 왼쪽요소로 처리방향만 다르다.
```javascript
// reduceRight() 를 활용하여 배열 요소의 순서를 뒤집기
function concat (accmulatedString, item) {
    return accmulatedString + item;
}

var words = ['the', 'quick', 'brown', 'fox '];
var sentence = words.reduceRight(concat);
print(sentence); // fox brown quick the
```
    
##### 2.5.2 새 배열을 반환하는 반복자 함수
- map()
    - forEach() 처럼 배열의 각 요소에 함수를 적용하는 함수이다.
    - 배열의 요소에 적용한 결과를 포함하는 새 배열을 반환한다.
```javascript
function curve (grade) {
    return grade += 5;
}

var grades = [10, 15, 20, 25, 30];
var newGrades = grades.map(curve);
print(newGrades); // 15, 20, 25, 30, 35
```

- filter()
    - every() 함수와 비슷하다.
    - 불린 함수를 만족하는 요소를 포함하는 새로운 배열을 반환한다.
```javascript
function isEven (num) {
    return num % 2 === 0;
}

function isOdd (num) {
    return num % 2 !== 0;
}

var nums = [];
for (var i = 0; i < 10; i++) {
    nums.push(i + 1);
}

var evens = nums.filter(isEven);
print(evens); // 2, 4 ,6 ,8

var odds = nums.filter(isOdd);
print(odds); // 1, 3, 5, 7, 9 
```
    

#### 2.6 이차원 배열과 다차원 배열
- 자바스크립트는 기본적으로 일차원 배열만 지원하지만 배열의 배열을 이용해 다차원 배열을 만들 수 있다.


##### 2.6.1 이차원 배열 생성
- 이차원 배열은 행과 열을 가진 스프레드시트 같은 구조이다.
- 자바스크립트에서 이차원 배열을 만드려면 배열을 만든 뒤 각 요소를 배열로 만들어야 한다.

가장 간단한 이차원 배열을 생성하는 방법
- 배열의 모든 요소가 undefined로 설정 된다.
```javascript
var twod = [];
var rows = 5;
for (var i = 0; i < rows; i++) {
    twod[i] = [];
}
```

"더글라스 크락포드의 자바스크립트 핵심 가이드" 에서 제공하는 실용적인 이차원 배열 생성 방법
- 자바스크립트 배열 객체를 함수로 확장한다.
- 배열의 행과 열의 개수를 설정하며 함수에 제공된 기본 값으로 모든 요소를 초기화 한다.
```javascript
// 2차원 배열을 생성하는 matrix 함수
Array.matrix = function (numrows, numcols, initValue) {
    var arr = [];
    for (var i = 0; i < numrows; i++) {
        var columns = [];
        for (var j = 0; j < numcols; j++) {
            columns[j] = initValue;
        }
        arr[i] = columns;       
    }
    return arr;
}

// matrix 함수를 활용한 생성 및 출력 예제
var nums = Array.matrix(5, 5, 0);
print(nums[1][1]); // 0 출력
```

선언과 동시에 이차원 배열을 정의하고 초기화하는 방법
- 다음과 같이 한 줄의 코드로 이차원 배열을 정의하고 초기화할 수 있다.
```javascript
var grades = [[89, 77, 55], [11, 22, 45], [11, 33, 48]];
print(grades[0][1]); // 77 출력
```

##### 2.6.2 이차원 배열 요소 처리하기
- 이차원 배열의 요소는 두가지 주요 패턴으로 처리한다.
- 1. 배열의 열을 기준으로 처리하는 방법
- 2. 배열의 행을 기준으로 처리하는 방법


배열의 열을 기준으로 처리하는 방법
- 중첩 for문을 사용한다.
- 외부 루프가 행을 처리하고 안쪽 루프가 열을 처리한다.

중첩 for문을 활용하여 평균을 구하는 예제이다.
```javascript
var grades = [[89, 77, 78], [76, 82, 11], [91, 55, 86]];
var total = 0;
var average = 0.0;

for (var row = 0; row < grades.length; row++) {
    for (var col = 0; col < grades[row].length; col++) {
        total += grades[row][col];
    }
    average = total / grades[row].length;
    print(`total = ${total}, average = ${average}`);
    total = 0;
    average = 0.0;   
}

// 출력 결과
// 81.33333..., 56.333333..., 77.333333...
```


배열의 행을 기준으로 처리하는 방법
- 중첩 for문을 사용한다.
- 외부 루프가 열을 처리하고 안쪽 루프가 행을 처리한다.

앞선 예제를 외부 루프가 열을 처리하고 내부 루프가 행을 처리하도록 변경한 예제이다.
```javascript
var grades = [[89, 77, 78], [76, 82, 11], [91, 55, 86]];
var total = 0;
var average = 0.0;

for (var col = 0; col < grades.length; col++) {
    for (var row = 0; row < grades[col].length; row++) {
        total += grades[col][row];
    }
    average = total / grades[col].length;
    print(`total = ${total}, average = ${average}`);
    total = 0;
    average = 0.0;
}
```

##### 2.6.3 들쭉날쭉한 배열
- 배열의 행이 포함하는 요소의 개수가 서로 다른 배열이다.
- 다른 프로그래밍 언어는 들쭉날쭉한 배열을 처리하기 어렵다
- 자바스크립트는 모든 행의 길이를 정확하게 알 수 있으므로 들쭉날쭉한 배열도 쉽게 처리가 가능하다.

```javascript
var grades = [[89, 77], [76, 82, 81], [91, 94, 89, 99]];
var total = 0;
var average = 0.0;

for (var row = 0; row < grades.length; row++) {
    for (var col = 0; col < grades[col].length; col++) {
        total += grades[row][col];
    }
    average = total / grades[row].length;
    print(`Student ${parseInt(row + 1)} average = ${average.toFixed(2)}`);
    total = 0;
    average = 0.0;
}

// 출력 결괴
// Student 1 average = 83.00
// Student 2 average = 79.67
// Student 3 average = 93.25
```
    
    
#### 2.7 객체를 요소로 포함하는 배열
- 배열은 객체도 요소로 포함할 수 있다.


Point 객체를 배열에 저장하고 이를 출력 하는 예제
- push 함수와 shift 함수를 활용하여 좌표를 추가 및 제거
```javascript
function Point (x, y) {
    this.x = x;
    this.y = y;
}

function displayPts (arr) {
    for (var i = 0; i < arr.length; i++) {
        print(`${arr[i].x}, ${arr[i].y}`);
    }
}

var p1 = new Point(1, 2);
var p2 = new Point(3, 5);
var p3 = new Point(2, 8);
var p4 = new Point(4, 4);
var points = [p1, p2, p3, p4];
for (var i = 0; i < points.length; i++) {
    print(`Point ${parseInt(i + 1)} : ${points[i].x}, ${points[i].y}`);
}

var p5 = new Point(12, -5);
points.push(p5);
print('After Push');
displayPts(points);
points.shift();
print('After Shift');
displayPts(points);

// 출력 결과
/*
Point 1: 1,2
Point 2: 3,5
Point 3: 2,8
Point 4: 4,4
After Push
1,2
3,5
2,8
4,4
12,-3
After Shift
3,5
2,8
4,4
12,-3
*/
```

#### 2.8 객체에 포함된 배열
- 객체에 복잡한 데이터를 저장할때 배열을 활용할 수 있다.
- 많은 자료구조들은 클래스로 구현 되었으며 클래스에 데이터를 저장할때 내부적으로 배열을 사용한다.

한 주 동안 관찰된 가장 높은 온도를 저장하는 객체
- 객체의 기능
    - 새 온도를 추가
    - 객체에 저장된 온도의 평균을 계산하는 기능
```javascript
function weekTemps () {
    this.dataStore = [];
    this.add = add;
    this.average = average;
}

function add (temp) {
    this.dataStore.push(temp);
}

function average () {
    var total = 0;
    for (var i = 0; i < this.dataStore.length; i++) {
        total += this.dataStore[i];
    }
    return total / this.dataStore.length;
}


var thisWeek = new weekTemps();
thisWeek.add(52);
thisWeek.add(55);
thisWeek.add(61);
thisWeek.add(65);
thisWeek.add(55);
thisWeek.add(50);
thisWeek.add(52);
thisWeek.add(49);
print(thisWeek.average()); // 54.875 출력
```

#### 2.9 연습문제
1. 객체에 학생들의 점수 집합을 저장하는 grades 객체 정의
- 점수를 추가하는 함수와 학생의 평균 점수를 출력하는 기능 구현
```javascript
function grades() {
    this.scores = [];
    this.add = function (score) {
        this.scores.push(score);
    };
    this.average = function () {
        return this.scores.reduce((result, data) => result + data, 0) / this.scores.length;
    };
}
```

2. 배열의 단어 집합을 저장한 뒤 배열의 내용을 정방향 또는 역방향으로 출력하는 기능 구현
```javascript
var words = ['abcd', 'bcde', 'cde', 'def'];
print(words); // 정방향
print(words.reverse()); // 역방향
```


3. 이차원 배열을 이용해 월간 온도 자료를 저장하도록 weeklyTemps 객체를 수정
- 월간 평균, 지정한 주의 평균, 모든주의 평균을 출력하는 기능 구현
```javascript
function WeeklyTemps () {
    this.dataStore = [[], [], [], []]; // 4주를 기준
    this.monthlyAverage = function () {
        /*
        var totalLength = 0;
        var total = this.dataStore.reduce((resultData, dataStore) => {
            totalLength += dataStore.length;
            return resultData + dataStore.reduce((result, data) => result + data, 0);    
        }, 0);
        return total / totalLength;
        */

        var weeks = this.weeksAverage();
        return weeks.reduce((result, data) => result + data, 0) / weeks.length;
    };
    this.targetWeekAverage = function (targetWeek) {
        return this.dataStore[targetWeek].reduce((result, dataStore) => result + dataStore, 0) / this.dataStore[targetWeek].length;
    };
    this.weeksAverage = function () {
        return this.dataStore.map((dataStore, index) => this.targetWeekAverage(index));
    };
}
```
    
    
    
    
    
    
    
    
