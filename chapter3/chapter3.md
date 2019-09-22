# 리스트


#### 3.1 리스트 ADT
- 리스트 ADT를 설계하려면 리스트의 정의, 프로퍼티, 동작, 리스트에 의해 수행되는 동작 등을 알야아한다.

리스트의 정의
- 순서가 있는 일련의 데이터 집합이다.
- 리스트에 저장된 각 데이터 항목을 요소 (Element) 라고 부른다
- 자바스크립트에서는 모든 데이터형이 리스트의 요소가 될 수 있다.
- 요소의 수에는 제한이 없다.
    - 하지만 일반적으로 사용하는 프로그램의 가용 메모리가 최대 요소 수가 된다.
- 요소가 없는 리스트를 빈 (Empty) 리스트 라고 한다.
- 저장된 요소의 수를 리스트의 길이 (Length) 라고 한다.
- 내부적으로 요소 개수를 listSize 변수에 저장한다.
- 요소를 리스트의 끝에 추가 (append) 하거나 기존 요소 뒤 또는 요소 앞부분에 삽입 (insert) 할 수 있다.
- 요소를 삭제 (remove) 할 수 있으며, 전체삭제 (clear) 를 할 수 있다.
- toString() 함수를 이용해 리스트의 모든 요소를 출력하거나 getElement() 함수로 현재 요소의 값만 출력할 수 있다.
- 위치를 가리키는 프로퍼티가 존재한다.
- front, end 프로퍼티가 존재한다.
- next() 함수로 현재요소에서 다음 요소로 이동할수 있으며, prev() 함수로 현재 요소에서 이전 요소로 이동할 수 있다.
- moveTo(n) 함수를 이용하면 n번째 위치로 한번에 이동 할 수 있다.
- currPos()는 리스트의 현재 위치를 가리킨다.
- ADT는 리스트는 어떻게 저장할지는 정의하지 않으며 dataStore라는 배열을 이용해 요소를 저장한다.



리스트 ADT

| 프로퍼티 | 설명 |
| --- | --- |
| listSize (프로퍼티) | 리스트의 요소 수 |
| pos (프로퍼티) | 현재 위치 |
| length (프로퍼티) | 리스트의 요소 수 |
| clear (함수) | 리스트의 모든 요소 삭제 |
| toString (함수) | 리스트를 문자열로 표현하여 반환 |
| getElement (함수) | 현재 위치의 요소를 반환 |
| insert (함수) | 기존 요소 위로 새 요소를 추가 |
| append (함수) | 새 요소를 리스트의 끝에 추가 |
| remove (함수) | 리스트의 요소 삭제 |
| front (함수) | 현재 위치를 리스트 첫 번째 요소로 설정 |
| end (함수) | 현재 위치를 리스트 마지막 요소로 설정 |
| prev (함수) | 현재 위치를 한 요소 뒤로 이동 |
| next (함수) | 현재 위치를 한 요소 앞으로 이동 |
| currPost (함수) | 리스트의 현재 위치 반환 |
| moveTo(함수) | 현재 위치를 지정된 위치로 이동 |


#### 3.2 List 클래스 구현
- 앞서 정의한 ADT를 활용해 List 클래스를 구현한다.
- 생성자 함수를 우선 구현한다.
```javascript
function List () {
    this.listSize = 0;
    this.pos = 0;
    this.dataStore = []; // 요소를 저장할 배열
    this.clear = clear;
    this.find = find;
    this.toString = toString;
    this.insert = insert;
    this.append = append;
    this.remove = remove;
    this.front = front;
    this.end = end;
    this.prev = prev;
    this.next = next;
    this.currPos = currPos;
    this.moveTo = moveTo;
    this.getElement = getElement;
    this.contains = contains;
    this.length = length;
}
```

##### 3.2.1 Append: 리스트에 요소 추가
- append() 함수는 리스트의 다음 가용위치 (listSize 변수의 값) 에 새 요소를 추가하는 함수이다.
- 요소를 추가한 뒤 listSize 를 1만큼 증가 시킨다.
```javascript
function append (element) {
    this.dataStore[this.listSize++] = element;
}
```


##### 3.2.2 Remove: 리스트의 요소 삭제
- remove() 함수는 List 클래스의 함수중 가장 구현하기 어려운 함수이다.
- 삭제 프로세스
    - 우선 리스트에서 삭제하려는 요소를 찾는다.
    - 요소를 삭제하고, 나머지 배열 요소를 왼쪽으로 이동시켜 요소가 삭제된 자리를 메워야 한다.
    - splice() 함수를 이용하면 이 과정을 쉽게 해결할 수 있다.


**삭제할 요소를 찾는 헬퍼함수 find()**
```javascript
function find (element) {
    var length = this.dataSource.lengh;
    for (var i = 0; i < length; i++) {
        if (this.dataSource[i] === element) {
            return i;
        }
    }
    return -1;
}
```

##### 3.2.3 Find: 리스트의 요소 검색
- find() 
    - 루프로 dataSource를 반복하며 원하는 요소를 검색한다.
    - 요소를 발견하면 요소의 위치를 반환한다.
    - 요소를 찾지 못할경우 -1을 반환한다.
    
- remove()
    - find() 함수의 반환값으로 에러를 감지할수 있다.
    - find() 함수의 반환값을 splice() 함수에 넘겨주어 원하는 요소를 삭제한뒤 dataSource 배열을 연결한다.
    - remove() 함수는 해당 요소를 삭제했다면 true를 반환하고, 삭제하지 못했다면 false를 반환한다.
    
```javascript
const NOT_FOUND = -1;
function remove (element) {
    var index = this.find(element);
    if (index === NOT_FOUND) {
        return false;
    }
    this.dataSource.splice(index, 1);
    this.listSize--;
    return true;
}
```

##### 3.2.4 Length: 리스트의 요소 개수
- length() 함수는 리스트의 요소 개수를 반환한다.

```javascript
function length () {
    return this.listSize;
}
```

##### 3.2.5 toString: 리스트의 요소 확인
- toString()
    - 리스트의 요소를 확인하는 함수이다.
    - 함수는 문자열이 아닌 배열 객체를 반환한다.
    - 하지만 배열을 반환하므로 현재 요소의 상태를 알 수 있다.
    
```javascript
function toString () {
    return this.dataSource;
}
```

###### 중간점검
- 현재까지 구현한 List 클래스가 잘 동작하는지 중간점검을 진행한다.
```javascript
// given
var names = new List();
names.append("괴도");
names.append("정곰");
names.append("라이코스");
names.append("마이펫");
names.append("흑곰");

print(names.toString());
names.remove("흑곰");
print(names.toString());

/*
출력 결과
괴도, 정곰, 라이코스, 마이펫, 흑곰
괴도, 정곰, 라이코스, 마이펫
*/
``` 

##### 3.2.6 Insert: 리스트에 요소 삽입
- insert()
    - 리스트의 기존 요소 뒤에 새로운 요소를 삽입하게 한다.
    - 헬퍼함수 find() 를 이용해 새 요소의 삽입 위치를 결정한다.
    - splice() 함수를 이용해 새 요소를 리스트에 추가한다.
    - listSize를 1만큼 증가 시키고 true를 반환한다.
    - 만약 실패했다면 false를 반환한다.
    
```javascript
function insert (element, after) {
    var insertPos = this.find(after);
    if (insertPos > -1) {
        this.dataSource.splice(insertPos + 1, 0, element);
        this.listSize++;
        return true;
    }
    return false;
}
```

##### 3.2.7 리스트의 모든 요소 삭제
- clear() 
    - delete 명령어로 모든 dataSource 배열을 삭제한 다음 빈 배열을 다시 만든다.
    - listSize와 pos를 0 으로 만든다.
        - 새 리스트의 시작 위치로 초기화 한다.
```javascript
function clear () {
    delete this.dataSource;
    this.dataSource.length = 0;
    this.listSize = this.pos = 0;
}
```

##### 3.2.8 Contains: 리스트에 특정값이 있는지 판단
- contains()
    - 어떤 값이 리스트에 포함되어 있는지 확인할때 사용하는 함수이다.
```javascript
function contains (element) {
    var length = this.dataSource.length;
    for (var i = 0; i < length; i++) {
        if (this.dataSource[i] === element) {
            return true;
        }
    }
    return false;
}
```
















