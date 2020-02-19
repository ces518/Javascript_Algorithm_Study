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

#### 5.3 Queue 클래스 사용하기: 스퀘어 댄스 파티에서 파트너 정하기
- 생략

#### 5.4 큐로 데이터 정렬하기
- 데이터를 정렬할 때도 큐를 사용할 수 있다.
- 여러 큐를 이용해 펀치 카드 정렬을 시뮬레이션 할수 있다.
- 이런 정렬 기법을 기수 정렬 (Radix Sort) 라고 한다.
- 기수 정렬이 가장 빠른 정렬 알고리즘은 아니지만 큐를 활용한 재미있는 방법을 보여준다.

- 기수 정렬은 두번의 과정을 걸쳐 데이터를 정렬한다. 0~99 사이의 정수 데이터가 있다고 가정하자.
```javascript
91, 46, 85, 15, 92, 35, 31, 22
```

- 기수정렬의 첫번째 과정을 거치면 데이터가 다음처럼 정렬된다.
    - 1의 자리수를 기점으로 정렬을 한다.
```javascript
0:
1: 91, 31
2: 92, 22
3:
4:
5: 85, 15, 35
6: 46
7:
8:
9:
```

- 이번에는 두번째 과정을 거치면 데이터가 다음처럼 정렬 된다.
    - 10의 자리수를 기점으로 정렬을 한다.
```javascript
0:
1: 15
2: 22
3: 31, 35
4: 46
5:
6:
7:
8: 85
9: 91, 92
``` 

- 정렬된 숫자들의 결과는 다음과 같다.
```javascript
15, 22, 31 ,35, 46, 85, 91, 92
```

- 큐를 이용해 이 알고리즘을 구현할 수 있다.
- 여기서 큐는 통의 역할을 하며 각 숫자당 한개 즉 9개의 큐가 필요하다.
- 나머지와 나눗셈 연산을 활용해 1의 자리 숫자인지 10의자리 숫자인지 구분할 수 있다.

- 다음은 1의 자리 숫자인지 10의 자리 숫자인지 구분해 큐에 숫자를 추가하는 함수이다.
```javascript
function distribute(nums, queues, n, digit) {
   for (var i = 0; i < n; i++) {
       if (digit == 1) {
           queues[nums[i]%10].enqueue(nums[i]);
       } else {
           queues[Math.floor(nums[i] / 10)].enqueue(nums[i]);
       }
   } 
}
``` 

- 다음은 큐에 저장된 숫자를 수집하는 함수이다.
```javascript
function collect(queues, nums) {
    var i = 0;
    for (var digit = 0; digit < 10; digit++) {
        while (!queues[digit].empty()) {
            nums[i++] = queues[digit].dequeue();
        }
    }
}
```

`배열의 내용을 출력하는 함수를 포함한 기수 정렬을 수행하는 전체 프로그램`
```javascript
function distribute(nums, queues, n, digit) {
   for (var i = 0; i < n; i++) {
       if (digit == 1) {
           queues[nums[i]%10].enqueue(nums[i]);
       } else {
           queues[Math.floor(nums[i] / 10)].enqueue(nums[i]);
       }
   } 
}

function collect(queues, nums) {
    var i = 0;
    for (var digit = 0; digit < 10; digit++) {
        while (!queues[digit].empty()) {
            nums[i++] = queues[digit].dequeue();
        }
    }
}

function dispArray(arr) {
    for (var i = 0; i < arr.length; i++) {
        putstr(arr[i] + " ");
    }
}
```

#### 5.5 우선순위 큐
- 큐에서 요소를 삭제할 때에는 먼저 삽입한 요소 부터 삭제된다.
- 하지만 선입 선출 방식이 아닌 우선순위와 같은다른 기준으로 요소를 삭제해야할 경우도 있다.
- 이럴 때에는 우선순위 큐 (Priority Queue)라는 자료구조를 이용해야 한다.
- 우선순위 큐는 요소의 우선순위를 기준으로 요소의 삭제 순서를 결정한다.
- 병원 응급실과 같은 상황이다.
- 병원 응급실의 대기실에는 예진 간호사가 환자를 검사한뒤 환자의 상태를 평가해 우선순위를 지정한다.
- 우선순위가 높은 코드를 받은 환자는 우선순위가 낮은 환자보다 먼저 진료를 받고, 우선순위가 동일할 경우 선입 선출 규칙을 따른다.

`환자 객체`
```javascript
function Patient (name, code) {
    this.name = name;
    this.code = code;
}
// code 는 환자의 우선순위를 나타내는 정수이다.
```
`dequeue 함수`
- 환자의 우선순위에 따라 요소를 삭제하도록 수정한다.
- 우선순위가 같을 경우 선입선출의 방식을 따른다.
```javascript
function dequeue () {
    var entry = 0;
    
    for (var i = 0; i < this.dataStore.length; i++) {
        if (this.dataStore[i].code < this.dataStore[entry].code) {
            entry = i;
        }
    }
    return this.dataStore[entry].splice(entry, 1);
}
```
> dequeue() 함수는 순차검색방법으로 우선순위가 가장 높은 코드(숫자가낮을수록 우선순위가 높음)를 찾는다.
- 큐에서 제거된 요소를 반환한다.


















