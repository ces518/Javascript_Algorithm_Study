# 스택
- 리스트는 데이터를 자연스럽게 나열한 구조이다.
- 리스트와 비슷하면서 보다 다양한 문제를 해결할 수 있는 스택 이라는 자료구조가 있다.
- 스택은 가장 윗부분에서만 자료의 추가와 삭제가 일어나므로 실행속도가 빠르고 구현이 쉬운 효율적인 자료구조다.

#### 4.1 스택
- 스택의 요소는 리스트로 구성되며, 탑(TOP) 이라 불리는 리스트의 한쪽 끝으로만 요소에 접근할수 있다.
- 구내식당에 쌓아둔 쟁반을 스택에 비유할 수 있다.
- 가장 위의 쟁반부터 이용해야하며 설거지를 끝내고 쟁반을 돌려놓을때는 이전에 쌓아둔 쟁반위에 올려두어야 한다.
- LIFO (Last In Fisrt Out) 의 자료구조이다.
- 스택의 탑에 있지 않은 요소에는 접근할 수 없다.
- 요소를 추가하거나 제거하는 두가지 주요 동작을 제공한다.
    - push, pop
- push 동작을 이용해 요소를 스택에 추가한다.
- pop 동작을 이용해 요소를 꺼낸다.
- TOP에 존재하는 요소를 확인하는 기능은 peek 이다.
- pop과 peek의 차이는 pop는 요소를 영구적으로 스택에서 제거하지만, peek은 요소를 제거하지않고 확인만할 수 있다.
- top 요소의 위치와 새 요소를 추가할 위치는 top 변수를 이용해 관리한다.
- 새 요소를 추가할때는 top 변수를 증가시키고, 요소를 제거했을 때는 top 변수를 감소시킨다.
- clear 프로퍼티는 스택의 모든요소를 삭제한다.
- length 프로퍼티는 스택에 포함된 요소의 수를 저장한다.
- 스택에 요소가 있는지 여부를 알려주는 프로퍼티도 존재한다.

#### 4.2 스택 구현
- 스택의 내부요소를 저장할 자료구조는 배열을 사용한다.

Stack 클래스의 생성자 함수
- dataStore는 스택의 요소를 저장하는 배열이다.
- top은 스택의 탑 정보를 유지하며 생성자에서는 top을 0으로 초기화 한다.
```javascript
function Stack () {
    this.dataStore = [];
    this.top = 0;
    this.push = push;
    this.pop = pop;
    this.peek = peek;
}
```

Push()
    - 새 요소를 스택에 추가하는 함수이다.
    - 탑 위치에 요소를 저장한 다음 빈 배열에서 빈 공간을 새로운 탑이 가르키도록 top 변수를 증가 시킨다.
```javascript
function push (element) {
    this.dataStore[this.top++] = element;
}
```

Pop()
    - Push() 의 반대동작
    - TOP의 요소를 반환하고 TOP변수를 감소시킨다.
```javascript
function pop () {
    return this.dataStore[--this.top];
}
```

Peek()
    - 배열의 top - 1 위치에 있는 요소에 접근하여 스택의 TOP 요소를 반환한다.
```javascript
function peek () {
    return this.dataStore[this.top - 1];
}
```

length()
    - 스택에 얼마나 많은 데이터가 저장되어 있는지 요소의 개수를 반환한다.
```javascript
function length () {
    return this.top;
}
```

clear()
    - top변수를 0으로 초기화하여 스택 전체 요소를 삭제한다.
```javascript
function clear () {
    this.top = 0;
}
```

Stack 클래스의 전체 코드
```javascript
function Stack () {
    this.dataStore = [];
    this.top = 0;
    this.push = push;
    this.pop = pop;
    this.peek = peek;
    this.clear = clear;
    this.length = length;
}

function push (element) {
    this.dataStore[this.top++] = element;
}

function pop () {
    return this.dataStore[--this.top];
}

function peek () {
    return this.dataStore[this.top - 1];
}

function clear () {
    this.top = 0;
}

function length () {
    return this.top;
} 
```


Stack 클래스의 구현을 테스트하는 프로그램
```javascript
var stack = new Stack();
stack.push('혜지');
stack.push('베어');
stack.push('괴도');
stack.push('정곰');
stack.push('마이펫');
stack.push('멍뭉덕');
print(`저장된 요소의 수 = ${stack.length()}`);
print(`현재 top 요소 = ${stack.peek()}`); // 멍뭉덕
var popped = stack.pop();
print(`pop으로 꺼낸 요소 = ${popped}`);
print(`현재 top 요소 = ${stack.peek()}`); // 마이펫
stack.clear();
print(`저장된 요소의 수 = ${stack.length()}`);
```


#### 4.3 Stack 클래스 이용하기
- 스택을 이용해 다양한 문제를 해결할 수 있다.
- 4.3 절에서는 스택으로 해결할 수 있는 여러 문제를 살펴본다.


##### 4.3.1 진법 변환
- 어떤 진법에서는 다른 진법으로 숫자를 변환할때 스택을 이용할 수 있다.

- 2진수부터 9진수 사이에만 동작한다.
    - 1. n의 가장 오른쪽 숫자는 n%b 이다. 이 값을 스택에 추가한다.
    - 2. n을 n/b으로 치환한다.
    - 3. n=0이 되고, 나머지가 없을때 까지 1번 2번 과정을 반복한다.
    - 4. 스택에 저장된 숫자를 모두 꺼내 변환된 숫자 문자열을 만든다.


`기수가 2~9사이인 수의 진법을 변환하는 함수`
```javascript
function mulBase (num, base) {
    var s = new Stack();
    do {
        s.push(num % base);
        num = Math.floor(num /= base);
    } while (num > 0);
    var converted = "";
    while (s.length() > 0) {
        converted += s.pop();
    }
    return converted;
}
```

##### 4.3.2 회문
- 앞으로 읽으나 뒤로 읽으나 같은 단어, 구절, 숫자를 회문 palindrome 이라고 한다.
- ex) dad, racecar

- 스택을 이용하여 문자열이 회문인지 여부를 판단할 수 있다.
```javascript
function isPalindrome (word) {
    var s = new Stack();
    for (var i = 0; i < word.length; i++) {
        s.push(word[i]);
    };
    var reverseWord = "";
    while (s.length() > 0) {
        reverseWord += s.pop();
    }
    return word === reverseWord;
};
```





