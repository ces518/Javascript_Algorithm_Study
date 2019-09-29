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

##### 3.2.9 리스트 탐색
- 리스트 탐색과 관련된 함수들이다.
- front()
    - 현재 위치를 나타내는 pos 를 0 으로 초기화한다.
- end()
    - 현재 위치를 리스트의 가장 마지막 요소를 가리키도록 초기화한다.
- prev()
    - 현재 위치에서 이전 요소를 가리키도록 변경한다.
- next()
    - 현재 위치에서 다음 요소를 가리키도록 변경한다.
- moveTo(position)
    - position에 해당하는 위치로 가리키도록 변경한다. 
- getElement()
    - 현재 위치의 요소를 반환한다.
```javascript
function front () {
    this.pos = 0;
}

function end () {
    this.pos = this.listSize - 1;
}

function prev () {
    if (this.pos > 0) {
        this.pos--;
    }
}

function next () {
    if (this.pos < this.listSize - 1) {
        this.pos++;
    }
}

function currPos () {
    return this.pos;
}

function moveTo (position) {
    this.pos = position;
}

function getElement () {
    return this.dataSource[this.pos];
}
```

```javascript
// given 
// 리스트 데이터 초기화
var names = new List();
names.append('자바');
names.append('스크립트');
names.append('알고리즘');
names.append('스터디');

names.front(); // 리스트의 0번째 요소를 가리키도록 초기화
print(names.getElement()); // 자바 출력

names.next(); // 현재 위치에서 다음 요소를 가리키도록 변경
print(names.getElement()); // 스크립트 출력

names.prev(); // 현재 위치에서 이전 요소를 가리키도록 변경
print(names.getElement()); // 자바 출력

names.end(); // 리스트의 가장 마지막 요소를 가리키도록 초기화
print(names.getElement()); // 스터디 출력
```

#### 3.3 리스트와 반복
- 반복자를 활용하면 List클래스의 내부 저장소를 직접 참조하지않고 리스트를 탐색할 수 있다.
- front(), end(), prev(), next(), currPos() 함수들을 이용해 반복자를 구현할 수 있다.
- 배열의 인덱스와 비교했을때 다음과 같은 장점이 있다.
    - 리스트 요소 접근시 내부 데이터 저장소가 무엇인지 알고있지 않아도 된다.
    - 리스트가 바뀌어도 반복자를 갱신할 필요가 없다.
    - List 클래스에 사용하는 데이터 저장소의 종류가 바뀌어도 이전과 같은 방식으로 요소에 접근이 가능하다.
    
`반복자를 이용해 리스트를 탐색하는 코드`
- front() 함수를 활용해 현재 위치를 리스트의 가장 앞으로 초기화한다.
- currPos() 함수가 리스트의 길이 보다 작을때 루프를 반복하고, 매 루프마다 next() 함수를 호출하여 현재 위치의값을 증가시킨다. 
```javascript
for (names.front(); names.currPos() < names.length(); names.next()) {
    print(names.getElement());
}
```

#### 3.4 리스트 기반 애플리케이션
- Redbox와 같은 비디오 대여상점 운영 시스템에서 리스트 활용 예시 이다.


##### 3.4.1 텍스트 파일 읽기
- 상점에 존재하는 비디오 목록을 프로그램으로 읽어오려면 파일의 데이터를 읽어야한다.
- 비디오 목록을 포함하는 텍스트 파일
```text
1. The Shawshank Redemption
2. The Godfather
3. The Godfather : Part 2
4. Pulp Fiction
5. The Good, the Bad and the Ugly
6. 12 Angry Men
7. Schindler's List
8. The Dark Knight
9. The Lord of the Rings : The Return of the King
10. Fight Club
11. Star Wats : Episode V - The Empire Strikes Back
12. One Flew Over the Cuckook's Nest
13. The Lord of the Rings : The Fellowship of the Ring
14. Inception
15. Goodfellas
16. Star Wars
17. Seven Samurai
18. The Matrix
19. Forrest Gump
20. City of God 
```

파일의 내용을 프로그램으로 읽기
- 텍스트 파일의 내용을 배열로 저장할때 개행 문자는 공백으로 치환된다.
- 문자열 비교시 공백이 문제를 일으킬수 있기때문에 배열의 각 요소에서 앞뒤 공백을 제거해준다.
```javascript
var movies = createArr('films.txt');
function createArr (file) {
    var arr = read(file).split('\n');
    return arr.map(movie => movie.trim());
}
```

##### 3.4.2 리스트로 상점 관리하기
- movies 배열을 리스트로 저장하기

```javascript
var movieList = new List();
movies.forEach(movie => {
    movieList.append(movie);
});
```

- displayList(list)
    - 상점에서 판매중인 영화 목록을 출력하는 함수이다.
    - displayList() 함수는 다음 예제에서 나올 Customer 객체에서는 잘 동작하지 않는다.
```javascript
function displayList (list) {
    for (list.front(); list.currPos() < list.length(); list.next()) {
        print(list.getElement());
    }   
};
```

- 개선된 displayList(list)
    - instanceof 연산자를 활용해 Customer 객체인지 확인한다.
    - Customer 객체라면 두 프러퍼티를 인덱스로 활용해 고객명과, 고객이 빌린 영화 명을 출력한다.
```javascript
function displayList (list) {
    for (list.front(); list.currPos() < list.length(); list.next()) {
        if (list.getElement() instanceof Customer) {
            print(`${list.getElement()['name']}, ${list.getElement()['movie']}`);
        } else {
            print(list.getElement());
        }
    }   
};
```

- 고객명과 고객이 빌린 영화명을 포함하는 고객 리스트
```javascript
function Customer (name, movie) {
    this.name = name;
    this.movie = movie;
};

var customers = new List();
```

- checkOut()
    - 고객이 영화를 대여하는 기능을 가진 함수
    - 고객명, 빌리려는 영화명이 필요하다.
    - 영화를 대여할수 있다면 영화목록에서 해당 영화를 삭제하고, 고객 리스트로 추가한다.
```javascript
function checkOut (name, movie, movieList, customerList) {
    if (movieList.contains(movie)) {
        var customer = new Customer();
        customerList.add(customer);
        movieList.remove(movie);
    } else {
        print(`movie 는 빌릴 수 없는 영화입니다.`);
    }
}
```



- 프로그램 실행 예제
```javascript
var movies = createArr('films.text');
var movieList = new List();
var customers = new List();

movies.forEach(movie => {
    movieList.append(movie);
});

print(`대여가능한 영화 목록 `);
displayList(movieList);

putstr(`고객명을 입력하세요: `);
var name = readLine();

putstr(`어떤 영화를 빌릴 껀가요`);
var movie = readLine();

checkOut(name, movie, movieList, customers);

print(`현재 대여한 고객 목록 `);
displayList(customers);

print(`대여가능한 영화 목록`);
displayList(movieList);
```


#### 3.5 연습문제
- 1. 현재 리스트의 모든 요소보다 클 때만 요소를 삽입하는 함수를 구현
```javascript
function append (list, element) {
    var isBiggest = true;
    for (list.front(); list.currPos() < list.length(); list.next()) {
        if (!list.getElement() < element) {
            isBiggest = false;
            break;
        }
    }
    if (isBiggest) {
        list.append(element);
    }
    return isBiggest;
}
```

- 2. 현재 리스트의 모든 요소보다 작을 때만 요소를 삽입하는 함수를 구현
```javascript
function append (list, element) {
    var isBiggest = true;
    for (list.front(); list.currPos() < list.length(); list.next()) {
        if (list.getElement() <= element) {
            isBiggest = false;
            break;
        }
    }
    if (isBiggest) {
        list.append(element);
    }
    return isBiggest;
}
```

- 3. 사람의 이름과 성별을 저장하는 Person 클래스를 구현, 최소 10개의 Person객체를 포함한느 리스트 생성
   리스트에서 같은 성별을 가진 사람을 모두 출력하는 함수를 구현
```javascript
function Person (name, isMan) {
    this.name = name;
    this.isMan = isMan;
}

var persons = new List();
persons.append(new Person('정곰1', false));
persons.append(new Person('정곰2', false));
persons.append(new Person('정곰3', false));
persons.append(new Person('정곰4', false));
persons.append(new Person('정곰5', false));
persons.append(new Person('정곰6', true));
persons.append(new Person('정곰7', true));
persons.append(new Person('정곰8', true));
persons.append(new Person('정곰9', true));
persons.append(new Person('정곰10', true));

function showSameGenderPersons (list, isMan) {
    for (list.front(); list.currPos() < list.length(); list.next()) {
        if (isMan === list.getElement()['isMan']) {
            print(`이름 = ${list.getElement()['name']} , 성별 = ${list.getElement()['isMan'] ? '남자' : '여자'}`);
        }
    }
}
```

- 4. 비디오 대여 상점 프로그램에서 고객이 대여한 영화를 대여된 영화 리스트로 추가하시오.
고객이 영화를 대여할때마다 대여된 영화 리스트를 출력하시오.
```javascript
var checkOutList = new List();
function checkOut (name, movie, movieList, customerList, checkOutList) {
    if (movieList.contains(movie)) {
        var customer = new Customer();
        customerList.append(customer);
        checkOutList.append(movie);
        movieList.remove(movie);
        displayList(checkOutList);
    } else {
        print(`movie 는 빌릴 수 없는 영화입니다.`);
    }
}
```

- 5. 비디오 대여 상점 프로그램에 반납함수를 추가하시오. 
고객이 영화를 반납하면 대여된 영화 리스트에서 영화를 삭제한 다음 이용할 수있는 영화 리스트를 추가하시오.
```javascript
function find (element) {
    var length = this.dataSource.length;
    for (var i = 0; i < length; i++) {
        if (this.dataSource[i] instanceof Customer) {
            if (this.dataSource[i].name === element) {
                return i;
            }        
        } else {
            if (this.dataSource[i] === element) {
                return i;
            }
        }
    }
    return -1;
}

function returnVideo (name, movie, movieList, customerList, checkOutList) {
    const index = customerList.find(customer => name === customer.name);
    if (index === -1) {
        return print(`${name} 은 존재하는 고객이 아닙니다.`);
    }
    customerList.moveTo(index);
    const customer = customerList.getElement();
    if (checkOutList.contains(movie) && customer.movie === movie) { // 체크아웃 목록에 존재하고, 고객이 대여한것이 맞을경우
        // 영화 반납
        movieList.append(movie);
        // 대여 리스트에서 삭제
        checkOutList.remove(movie);
        // Customer 에서 null로
        customer.movie = null;
        // 영화목록 출력
        displayList(movieList);
    } else {
        print(`${movie} 는 대여한 영화가 아닙니다.`);
    }   
}
```

















