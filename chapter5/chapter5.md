# 큐
- 큐는 리스트의 일종으로 끝부분으로 데이터가 삽입되고, 앞부분에서는 데이터가 삭제되는 자료구조이다.
- 선입선출의 자료구조이다.
- 운영 체제의 프로세스 처리순서, 프린트 스풀러 등 대기줄의 애플리케이션에서 큐를 사용한다.

#### 5.1 큐 동작
- 큐에 요소를 삽입하거나 삭제하는 것이 큐의 두가지 주요 동작이다.
- 요소를 삽입하는 것을 인큐 enqueue, 요소를 삭제하는 것을 데큐 dequeue 라고 한다.
- 인큐는 큐에 끝부분에 요소를 추가하며 데큐는 큐의 앞부분에서 요소를 삭제한다.
- 큐의 앞부분에 있는 요소를 확인할 수 있는 기능을 피크 peek라고 한다.
    - 앞부분에 있는 요소를 반환하지는 않는다.
- 큐의 요소의 갯수는 length 프로퍼티를 사용한다.
- 전체삭제는 clear 이다.

#### 5.2 배열 기반의 Queue 클래스 구현
- 배열을 이용하면 Queue클래스를 간단하게 구현할 수 있다.
- 자바스크립트에서는 push함수, shift 함수 등의 기능을 제공한다.
    - push: 가장 마지막에 데이터 추가
    - shift: 배열 앞부분에서 데이터를 삭제
   
`push()`
```javascript
names = [];
names.push('정곰');
names.push('미련');
print(names); // 정곰,미련
``` 

`shift()`
```javascript
names.shift();
print(names); // 미련
```

`Queue 클래스의 생성자`
```javascript
function Queue () {
    this.dataStore = [];
    this.enqueue = enqueue;
    this.dequeue = dequeue;
    this.front = front;
    this.back = back;
    this.toString = toString;
    this.empty = empty;
}
```

`enqueue()`
- 큐의 끝부분에 요소를 추가한다.
```javascript
function enqueue(element) {
    this.dataStore.push(element);
}
```

`dequeue()`
- 배열의 앞부분에서 요소를 삭제한다.
```javascript
function dequeue() {
    return this.dataStore.shift();
}
```

`front()`
- 큐의 앞부분의 저장된 요소를 확인한다.
```javascript
function front() {
    return this.dataStore[0];
}
```

`back()`
- 큐의 뒷부분의 저장된 요소를 확인한다.
```javascript
function back() {
    return this.dataStore[this.dataStore.length - 1];
}
```

`toString()`
- 큐의 모든 요소를 출력한다.
```javascript
function toString() {
    var retStr = '';
    var length = this.dataStore.length;
    for (var i = 0; i < length; i++) {
        retStr += this.dataStore[i] + '\n';
    }
    return retStr;
}
```

`empty()`
- 큐가 비었는지 확인한다.
```javascript
function empty() {
    if (this.dataStore.length === 0) {
        return true;
    } else {
        return false;
    }
}
```