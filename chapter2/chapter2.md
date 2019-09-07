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



