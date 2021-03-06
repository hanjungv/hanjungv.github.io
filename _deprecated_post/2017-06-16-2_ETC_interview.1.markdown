---

layout: post
title: "(ETC) 면접준비하기..[1/2]"
category: ETC

---

### 왜?
언젠가 한번 기억 저너머에 남아있는 기초 CS지식을 꺼내 복습해야겠다라고 생각했었는데 면접 준비 겸 장기적으로 다시 볼 수 있게 기술면접을 준비해 보려 합니다.

### OOP
Q. Class와 객체의 차이가 뭘까요?<br/>
Q. OOP 개념을 설명해 보세요<br/>
Q. 좋은 코드란 무엇일까요?<br/>
Q. 오버로딩 오버라이딩 차이가 뭘까요?<br/>
Q. 생성자와 소멸자<br/>
Q. 메모리를 allocation, 해제하는 것 코딩<br/>

* 객체지향 개념 설명
    * 객체지향(Object Oriented)라는 의미. 말 그대로 객체를 위주로 사용하여 프로그래밍을 하겠다는 말이다.
    * 먼저 이 객체지향을 왜 쓰는지에 대해 부족한 소양으로 유추해 보면 개발을 하는 우리의 환경은 여러 사람이 한 프로젝트를 수행하게 되고 이런 개발 되는 프로젝트는 지속적으로 변화하고 발전이 되어야 합니다. 또한 초기개발비용보다 유지비용이 크다. 그렇다면 협업이 쉽고 유지비용이 적도록 코딩을 해야한다는 것을 목표로 삼을 수 있다.
    * 자동차를 예로 들어보자!
        * 객체(Object) : 클래스의 Instance이다. 클래스가 실체로 만들어 진 것을 의미한다. 상태, 행위를 갖는다. BMW, 벤츠, 아우디 등 실제 차를 의미할 수 있다.
        * 클래스(Class) : 동일한 행위와 속성을 갖는 객체를 만들어 내는 틀을 의미한다. 자동차는 핸들, 바퀴, 움직이고 멈추고 등 공통적으로 하는 행동을 갖게 된다. 한 개체로 부터 공통 개념을 추출 하는 것을 **추상화**라고 한다.
        * 객체지향의 특징
            * 캡슐화(Encapsulation) : 객체에 관한 내용을 캡슐에 넣어 내부를 볼 수 없게 하는 것을 의미합니다. 내부로직을 안보이게 하여 보안성의 의미도 있지만 자동차를 운전할 때 엔진이 어떻게 작동하고 연소가 어떻게 되고를 알지 못해도 자동차를 운전할 수 있듯이 굳이 알지 못해도 사용할 수 있는 메서드 들을 하나의 작동으로 묶어 놓는 것이라고 생각할 수도 있을 것 같다.
                * private : 자기 클래스 내부의 메서드에서만 접근 허용
                * protected : 자기 클래스 내부 또는 상속받은 자식 클래스에서 접근 허용
                * public : 모든 접근을 허용한다
            * 상속성(Inheritance) : 객체간의 관계를 부여하여 사용. 가지고 있는 특성을 그대로 이어받아 사용할 수 있다. 코드의 재사용성이 증가하고 간결해 집니다.
            * 다형성(Polymorphism) : 같은 이름의 멤버 함수가 서로 다르게 행동이 가능해 집니다.
                * 오버로딩(Overloading) : 매개변수의 갯수나 매개변수의 타입을 다르게 하여 같은 이름의 메서드가 다르게 행동하게 하는 것, 이를 통해 개발자들이 무한히 겪는 변수명 짓기의 고통이 조금이라도 줄어 들 수 있다. 직관적인 코드를 얻을 수 있다.
                * 오버라이딩(OverRiding) : 부모에게 상속받은 함수를 자식에서 변경하여 사용하는 것을 의미합니다. 이 때는 메서드의 이름이 같거나, 매개변수, 리턴타입이 같아야 합니다.
    * 고로! 결론은 **캡슐화, 상속, 다형성을 통해 코드의 재사용을 높이고 유지보수를 감소 시키는 장점을 얻기 위해서 객체 지향적 프로그래밍을 하는 것이다** 라고 표현 할 수 있을 것 같습니다.

* 좋은 코드란 뭐라고 생각하는가?
    1. 가독성이 좋은 코드, 다른 사람이 내가 짠 코드를 보고 쉽게 이해할 수 있으면 좋은 코드라 생각한다.
    2. 변수명을 성의 있게, 의미 있게 지어야 한다고 생각한다. 위에 말한 조건과 비슷한 의미라 생각한다.
    3. 주석을 남기되 읽어서 직관적으로 이해가 가는 것은 피하는 것이 좋을 것 같다. 코드에 글이 많아진다.
    4. if ~ else ~ 같은 코드를 쓸 때 긍정과 부정 순으로 조건문을 짜는게 좋다고 한다. 직관적이다.
    5. goto문 같이 스파게티 코드를 야기 하는 문법은 피하는 것이 좋다.
    6. 코드량을 줄이는 것이 좋다고 생각한다. 짧을 수록 에러량이 준다 라는 것은 통설인것 같다. 하지만 이런 짧은 코드가 직관적이지 않다면 직관적인 코드가 더 좋은 것 같다.

* 생성자와 소멸자?
    * 생성자와 소멸자는 객체가 생성될 때, 소멸될 때 작동하는 코드이다.
    * 생성자는 객체의 생성과 동시에 초기화를 해주기 때문에 은닉성과 안정성을 보장하기 쉽다.

* 메모리를 할당, 해제하는 것
    * C의 경우 malloc, free를 사용
    ```c
    int * ptr = (int *) malloc(size);
    free(ptr);
    ```

    * C++의 경우 new, delete를 사용한다.
    ```cpp
    int * ptr1 = new int; 
    int * ptr2 = new int[10]; 
    delete ptr1; 
    delete []ptr2; 
    ```

    * JavaScript 같은 경우에는 자동으로 할당이 되고 해제는 **가비지 컬렉션**의 형태로 이뤄 진다고 한다. 모질라 페이지에 나온 설명에 의하면 가비지 컬렉션은 참조하는 횟수를 세어 해제하는 것이다. 참조하는 횟수가 0이라면 다른 곳에서 어느곳에서도 참조하지 않는 다는 것을 의미하고 이것을 해제한다. 하지만 서로 참조를 하여 순환이 발생할 경우 이 문제를 해결할 수 없다. 


### Data Structure
Q. 리스트, 스택과 큐에 관해 설명해보라.<br/>
Q. vector와 list의 차이점과 특징을 설명해 보라. <br/>
Q. linked list와 map, hashmap의 특징 <br/>
Q. 현재 자신이 알고 있는 정렬 방법에 대해서 판서하며 설명해 보시오. <br/>
Q. 소팅 알고리즘을 슈도 코드로 구현하되, 변수를 사용하지 않고 해보세요.<br/>
Q. pseudo 코드로 이진트리를 탐색하고 최적화시키기<br/>
Q. 원형 스택 공간 처리문제 <br/>

* Array vs Linked List
* Stack / Queue
* vector vs list
    * vector는 연속적인 메모리 할당을 한다. 포인터를 포함하지 않는다. 중간 값을 제거하는데 O(n). 미리 할당하여 사용
    * list는 메모리 할당이 연속적이지는 않다. 다음과 이전을 가리키는 포인터를 포함한다. 중간 값을 제거하는데 O(1). 미리 메모리를 할당하지 않음
* linked list vs map vs hashmap
    * linkedlist
    * map : C++같은 경우 completely binary search tree로 구성(red-black tree). insert, delete가 O(logn)
    * hashmap : 
* Sorting
    * Bubble : O(n^2)의 시간복잡도를 갖는다. N크기의 배열을 N번 순회한다. 한번 순회할 때 마다 맨 뒤의 숫자는 제일 큰 값이 된다. 그러므로 ArraySize - i 번 순회한다. 
    ```cpp
    int* bubbleSort(int *bubbleData){
        for(int i =0 ; i<ARRSIZE; i++){
            for(int j =0; j<ARRSIZE - i; j++){
                if(bubbleData[j] > bubbleData[j+1]){
                    swap(bubbleData[j],bubbleData[j+1]);
                }
            }
        }
        return bubbleData;
    }
    ```
    * Selection : 현재 인덱스를 기준으로 뒤로 남은 배열중 가장 작은 값을 현재 인덱스에 넣게 된다. 이 경우에도 O(n^2)의 시간 복잡도가 된다.
    ```cpp
    int* selectionSort(int *selectionData){
        for(int i = 0 ; i<ARRSIZE; i++){
            int minIdx = i;
            int minVal = selectionData[i];
            for(int j = i+1; j < ARRSIZE; j++){
                if(minVal > selectionData[j]){
                    minVal = selectionData[j];
                    minIdx = j;
                }
            }
            swap(selectionData[i], selectionData[minIdx]);
        }
        return selectionData;
    }
    ```

    * Insertion : 이미 채워진 상태에서 소팅을 할 때 사용된다. 소팅할 데이터가 적은 양일 때 사용 성능이 좋다고 알려져있다. Best일 때는 O(n)이지만 Worst일 때는 O(n^2)이다. 내 앞 데이터들을 비교하며 인덱스의 값이 들어갈 위치를 찾게 된다. Random Access가 안되는 경우에 Optimal 방법이다.

    ```cpp
    int* insertionSort(int insertionData[]){
        for(int i = 1; i < ARRSIZE; i++){
            for(int j = i - 1; j >= 0; j--){
                if(insertionData[i] < insertionData[j]){
                    swap(insertionData[i], insertionData[j]);
                } else{
                    break;
                }
            }
        }
        return insertionData;
    }
    ```
    * Quick : Merge Sort와 마찬가지로 Devide & Conquer의 전략을 갖는다. 랜덤한 pivot을 갖고 Devide를 하게 된다. 이후 pivot을 기준으로 Left에서는 pivot보다 큰 값, Right에서는 pivot보다 작은 값을 찾아 swap 시켜준다. 이런 경우 pivot이 제일 왼쪽 인덱스 값에 고정이 된다면 O(n^2)이란 수행시간을 갖게 되는데 이런 경우는 거의 없다. 보통 O(nlogn)의 수행시간을 갖는다. 밑 코드는 Inplace Quick Sort를 구현한 코드이다.
    
    ```cpp
    void QuickSort(int lo, int hi, int *a){
        if (hi - lo < 1) return;
        int pivot = a[(hi+lo)/2];
        int i = lo, j = hi;
        while (i <= j) {
            while (a[i] < pivot) ++i;
            while (a[j] > pivot) --j;
            if (i > j) break;
            swap(a[i], a[j]);
            ++i, --j;
        }
        QuickSort(lo, j, a);
        QuickSort(i, hi, a);
    }
    ```
    * Merge : Quick Sort와 마찬가지로 Devide & Conquer의 전략을 갖는다. 

    ```cpp
    #define Len 10
    void mergeArray(int *arr,int l,int r){
        int temp[Len] = {0, };
        int mid = (l+r)/2, i = l, j = mid+1, totalIdx = l;
        while(i<=mid && j <= r){
            if(arr[i] <= arr[j]){
                temp[totalIdx] = arr[i];
                i++;
            } else{
                temp[totalIdx] = arr[j];
                j++;
            }
            totalIdx++;
        }
        for(i; i<= mid; i++,totalIdx++){
            temp[totalIdx] = arr[i];

        }
        for(j; j<= r; j++,totalIdx++){
            temp[totalIdx] = arr[j];
        }
        for(int a = l; a <= r ; a++){
            arr[a] = temp[a];
        }
    }
    void devideArray(int *arr, int l, int r) {
        int mid = (l + r) / 2;
        if (l < r) {
            devideArray(arr,l,mid);
            devideArray(arr,mid+1,r);
            mergeArray(arr, l, r);
        }
    }
    ```
    * Heap : 
* BFS / DFS

### Algorithm
Q. MST 알고리즘 설명해보세요!<br/>
Q. AVL-TREE, Red-Black Tree 설명!<br/>
Q. string += operation 칠판에 구현 <br/>
Q. 1~1000의 숫자중 중복 가능하게 1000개의 숫자를 뽑았을때, 이들 중 중간값을 묻는 문제였습니다.<br/>
Q. 1부터 100까지 더하는 프로그램을 칠판에 작성해보세요.<br/>
Q. atoi함수 구현<br/>
Q. 100! = 100 * 99 * ... * 2 * 1 = xx…x00..0 = xx…x * 10^n, 이때 n은? <br/>

### Network
Q. OSI7 계층, TCP, UDP 장단점 설명해 보세요!<br/>
* 물리
* 데이터링크 : MAC
* 네트워크 : IP
* 전송 : TCP/UDP
    * TCP는 연결형, UDP는 비연결형. UDP는 포트번호만 보고 송수신. 매우 빠르다. 신뢰성은 낮다
* 세션 : 통신세션구성, 포트번호
* 표현 : 포맷변환
* 응용 : 사용자가 네트워크에 접근하게 해주는 계층, HTTP
Q. TCP 3-way hand shaking이란?<br/>
* 3-way hand shaking : TCP 3 Way Handshake는 TCP/IP프로토콜을 이용해서 통신을 하는 응용프로그램이 데이터를 전송하기 전에 먼저 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정을 의미한다.
* 4-way hand shaking : TCP 연결을 종료하기 위한 절차이다.
    * [STEP 1] 클라이언트가 연결을 종료하겠다는 FIN플래그를 전송한다.
    * [STEP 2] 서버는 일단 확인메시지를 보내고 자신의 통신이 끝날때까지 기다리는데 이 상태가 TIME_WAIT상태다.
    * [STEP 3] 서버가 통신이 끝났으면 연결이 종료되었다고 클라이언트에게 FIN플래그를 전송한다.
    * [STEP 4] 클라이언트는 확인했다는 메시지를 보낸다.
    * Client에서 세션을 종료시킨 후 뒤늦게 도착하는 패킷이 있다면 이 패킷은 Drop되고 데이터는 유실될 것입니다. 이러한 현상에 대비하여 Client는 Server로부터 FIN을 수신하더라도 일정시간(디폴트 240초) 동안 세션을 남겨놓고 잉여 패킷을 기다리는 과정을 거치게 되는데 이 과정을 "TIME_WAIT" 라고 합니다.
    * 출처: http://mindnet.tistory.com/entry/네트워크-쉽게-이해하기-22편-TCP-3-WayHandshake-4-WayHandshake

Q. rtp와 rtcp 차이점은?<br/>
Q. HTTP 통신 원리
* 클라이언트에서 요청(request)를 보내면 서버는 요청을 처리해서 응답(response)한다


### Database
Q. 써본 DB가 뭐고 장단점 들을 말해보라<br/>
Q. 쿼리가 들어올 때, 어떻게 해야 효과적으로 저장할 수 있나요?<br/>
Q. ACID란?
Q. 인덱스가 어떤 구조로 이뤄져 있나요?
Q. 스키마란?

### Web part
Q. GET과 POST의 차이<br/>
Q. 웹 에서 오류코드 (ex. 404, 500, ...)들을 아는 대로 다 말하고 설명!<br/>
Q. 브라우저에 naver.com 쳤을 때 어떻게 작동하나요?(자주 나오나 보다)<br/>
Q. 알고있는 Design pattern 설명<br/>
Q. 세션과 쿠키의 차이점<br/>
Q. RESTful의 의미가 뭘까요?<br/>
Q. UI와 UX의 차이는 뭘까요?<br/>
Q. 프론트엔드의 성능을 개선하기 위해 어떤 방법을 사용했나<br/>
Q. 프론트엔드에서 사용했던 디버깅 방법은?

* get과 post의 차이
    * HTTP를 통한 전송 방식
    * get은 가져오는 것, post는 수행하는 것
    * get은 url에 내용이 붙어서 이동, (IE에서)길이의 제한이 있다. 주로 서버의 값을 가져오는 용도, 값을 변경하는데 크게 쓰이진 않는다.
    * parameter에 따라 페이지의 내용이 변경되는 경우에 많이 쓰인다. 암호, 파일 같은 것을 전달하는데 적절하지 않다.
    * post는 실제 서버에 내용이 변경되는데 많이 사용. 길이의 제한이 없다.

* HTTP 응답코드
    * 200 : 정상
    * 304 : 요청한 리소스가 마지막 요청 이후 변경된 적이 없기 때문에 기존 클라이언트의 로컬 캐시 리소스를 사용하도록 알려줌.
    * 401 : HTTP 인증(BASIC 인증, DIGEST 인증) 정보가 필요함을 알려줌. 처음엔 다이얼로그, 다음엔 실패
    * 404 : Not Found, 이 에러는 클라이언트가 요청한 문서를 찾지 못한 경우에 발생함. URL을 다시 잘 보고 주소가 올바로 입력되었는지를 확인함. 
    * 500 : Internal Server Error, 이 에러는 웹 서버가 요청사항을 수행할 수 없을 경우에 발생함 
    * 503 : 서버가 일시적으로 요청을 처리할 수 없음.
    * 등등..많다

* url을 입력하고 브라우저에 사이트가 불러지는 원리
    * Ruby on Rails를 예로 들었을 때 url을 유저가 브라우저에서 입력할 경우 브라우저는 웹서버에 요청을 보낸다.
    * Rails router를 거쳐 controller에 request가 도착
    * Model단에서는 해당 url의 Data Object를 가져오고 View단에서는 열심히 렌더링을 한다.
    * 그리고 response를 보낸다.
    * 실제로 웹 브라우저에서 웹 페이지를 띄우는 것은 좀 더 복잡한 원리라 알고 있다. HTML과 CSS, JS를 파싱하여 DOM객체를 만들고 트리구조로 만든다. 아무튼 이러한 내용은 여기에 친절한 번역본이 있다.
    * [http://d2.naver.com/helloworld/59361](http://d2.naver.com/helloworld/59361)

* Design pattern
    * MVC(MODEL / VIEW / CONTROLLER)
        * MVC패턴은 Application을 3가지 역할로 나누어 보는 디자인 패턴이다. 각각 Model, View, Controller로 구분 할 수 있다.
        * Model : 모델에 변화가 있을 때 컨트롤러에게 알려주게 됨. DB와 연결되어 있어 DB에 Object를 보내고 받고 한다.
        * View : 사용자가 직접 마주하는 부분이다. 웹에서는 주로 뷰를 구성하는 파일이 HTML, CSS, JS등이 있다. 
        * Controller : 모델과 뷰 사이에서 전체적인 통제를 하게 된다. 새로운 request가 view단에서 요청이 될 경우 model에 요청할 일이 있으면 controller에서 model에 요청하게 된다. 모델에 업데이트가 있을 경우 View단에 새롭게 렌더링을 할 때 요청을 하는 등 중간 관리자 역할을 하게 된다.
    * FLUX(React Redux 에서 잠시 접했던.)
        * Model과 View의 관계가 넘나 많아져 확장이 점점 힘들어지고 복잡도 또한 기하급수적으로 증가
        * Dispatcher, Store, View로 구성되어지고 단방향데이터 흐름이다.
        * 디스패처는 모든 데이터 흐름을 관리하는 허브 역할을 한다. 액션이 발생하면 디스패처로 메세지가 전달되고 디스패처에 등록된 콜백함수가 이 메세지를 스토어에 전달한다.
        * 메소드를 호출 할 때 데이터 묶음을 인수로 전달한다 이 데이터 묶음을 액션이라 한다.
        * 스토어는 상태를 저장한다. 자바스크립트의 Object와 개념이 비슷하다. 
        * 뷰는 MVC에서 하던 뷰의 역할을 넘어서 컨트롤러의 셩격 또한 가지고 있다. 뷰 레이어가 중첩될 때 최상위 뷰는 스토어에서 데이터를 가져와 하위 뷰에 전달해주는 역할 또한 한다.
        * 참조 [http://webframeworks.kr/tutorials/react/flux/](http://webframeworks.kr/tutorials/react/flux/)

* 세션과 쿠키의 차이점
    * 쿠키는 저장하는 곳이 클라이언트, 세션은 서버
    * 쿠키는 텍스트로 저장, 세션은 Object형태
    * 쿠키의 저장용량은 한정적(브라우저에 따라 다름), 세션은 서버에서 허용하는대로 가능
    * 세션은 클라이언트단과 서버단의 연결이 지속적으로 유지되고 있는 상태를 말한다. 
    * 쿠키는 브라우저가 완전이 종료되면 사라진다.
    * 주로 쿠키와 세션은 동일한 역할을 하게되는데 저장되는 곳에서 크게 차이가 나는 정도이다.
    * 클라이언트단에서 서버단과 연결이 되었을 때 세션ID를 만들고 세션 ID는 쿠키에 저장되어서 브라우저에서 가지고 있게됩니다. 로그인을 하게 되면 이 쿠키에서 ID정도가 있는지 확인을 하면 됩니다. 

* RESTful하게 설계된다는 것은 무엇일까?
    * 먼저 REST 아키텍쳐는 HTTP의 창시자가 만든 개념이다. HTTP를 제대로 활용 못하고 있다는 것에서 시작한다.
    * 자원을 정의하고(Resource), 행위를 정의하고(Verb), 행위의 내용을 정의하는데 HTTP의 특성을 활용한다.
    * 기본적으로 메서드는 HTTP메서드를 사용하고 CRUD각각에 POST, GET, PUT, DELETE를 사용한다.
    * URI를 설계할 때 동사보단 명사로 사용한다. 그리고 리소스는 복수형 명사로 표현한다.
    * 등등 내용이 많지만..

* UI / UX의 차이는 뭘까?
    * User Interface / User experience, UX가 좀 더 상위 개념. 유저가 경험한 모든 것들이 UX의 범위에 포함된다.

### OS
Q. 힙 / 스택영역설명<br/>
Q. IPC방법에 대해 간단히 설명해보세요!<br/>
Q. 쓰레드, 프로세스에 대한 설명 <br/>
Q. 64비트와 32비트의 차이점은 무엇인가요?<br/>
Q. 64bit 운영체제가 기존 운영체제보다 빠르다고 생각하는지. 그 이유는? <br/>
Q. 멀티스레드 개발에서 일관성을 보장해주는 방식<br/>
Q. memory fragmentation이란?<br/>
Q. 쓰레싱, 페이지 폴트, 버츄얼 메모리란?<br/>

* Heap / stack 영역
    * 프로세스가 되면 메모리를 각각 할당해 준다. 주로 데이터영역, 힙영역, 스택영역으로 나누어진다.
    * 스택 : 지역변수, 매개변수
    * 힙 : 동적할당 
    * 데이터 : 전역변수, static변수
* IPC (Inter Process Communication)
    * shared memory
        * 특징
            * 처음에만 시스템콜을 요청해 주기 때문에 속도가 매우 빠르다.
            * sync와 Protection에 관한 이슈가 있다.
            * Physical 메모리 공유 방법에 속한다.
    * message passing
        * 공유되는 부분이 없이 `send`와 `receive`를 통해 공유하게 된다.
        * Establishing link
            * Direct하게 통신 : process의 이름을 항상 넣어줘야 함. target id가 바뀔 수도 있고 여러가지 문제가 생길 수 있다.
            * Indirect하게 통신 : mailbox(unique한 id를 가진)를 만들어서 메일박스에 넣어주면 OS를 통해 알아서 가져가줌
        * 특징
            * Logical 메모리 공유 방법에 속한다.
            * 작은 양의 Data를 공유하는데 적절한 방법이다.
            * 매번 시스템 콜을 호출하기에 시간이 오래걸릴 수 있다.
            * 프로그래밍이 쉽다.
            * 컴퓨터 간 communication에 적합하다.



### Project 내용
Q. jQuery가 순수 JavaScript에 비해 단점이 뭐가 있을까?<br/>
Q. AWS 사용했던 것 설명 해보면?
* AWS
    * EC2 : 하나의 컴퓨터를 사서 선호하는 OS, 환경등을 구축해서 서버로 사용할 수 있다. rails의 passenger라는 젬을 이용하여 서버를 돌려 주었다. nginx를 이용하였는데 nginx는 웹서버로 빠르다고 한다. nginx는 event-driven이고 비동기적이라고 한다. 이러한 특징은 노드 JS에서도 찾을 수 있는데..아무튼 기존 절차적으로 block하여 기다리기보다 요청을 보내면 콜백함수에서 알아서 수행해줘서 하기 때문에 매우 빠르다 한다.
    * Route53 : 도메인 이름으로 ip주소를 바꿔주는 서비스이다. 라우트 53은 추가적으로 여러 기능을 제공하는데 하나의 도메인에 여러 ip가 할당 되어있을경우 서버의 상태를 체크해줘서 장애상태인 ip를 제외하고 관리한다. 또한 여러 ip 를 두었을 때 요청을 받을 경우 가장 빠른 응답으로 보여주게 된다.
    * S3 : Simple Storage Service의 줄임말. 파일을 저장하는 스토리지이다. 개별로 파일은 최대 5TB까지 저장가능하고 총 저장 용량에는 제한이 없다. 파일명이 유사하게 되면 같은 곳에 저장이 되어 성능이 떨어 지게 될 수 있다. prefix를 다양하게 하면 해싱되어 여러 곳에 분산 저장을 하여 빠르게 쓸 수 있다.
    * SQS : 메세지 큐 대기열 서비스이다. 단순히 enqueue / dequeue만 가능하다. 동시에 DB에 접근을 하지 못하게 하기 위해서 사용했다. FIFO로 순서를 주었다. 
* jekyll이 뭐에영?

#### 네**
Q. Ruby on Rails를 공부했던 이유? 장점이 뭐가 있는가?<br/>
Q. 마지막으로 진행하던 프로젝트는 완성이 되었는가?<br/>
Q. 사용된 추천 알고리즘에 대해 설명해 볼 수 있는가?<br/>
Q. 최근에 읽은 책은 무엇인가요?<br/>
Q. 이전 프로젝트에서 어떤 갈등이 있었고, 그 문제를 어떻게 해결했나요? 구체적인 사례를 들어 설명해 주세요.<br/>
Q. AWS EC2, S3, Route53, SQS, EBS 등에 대해 설명해보시오<br/>

* Ruby On rails 의 장점이라 생각한 것
    * Active Record라는 ORM을 제공한다. DB구성을 빠르게 할 수 있었다.
    * MVC모델에 맞춰서 확고하게 역할이 구분되어있다.
    * 초기 러닝커브가 낮다.
    * 웹을 처음 공부하는데 있어서 매우 쉽게 접근할 수 있었다.
    * 로그인 같은 초기에 구현하기 어려운 것들을 gem이란 라이브러리를 통해 쉽게 구현할 수 있게 한다.

* 확장질문
    * Active Record가 뭔가요?
        * RDBMS의 테이블을 SQL을 직접 사용하지 않고 조작하게 해 줍니다.
        * 데이터형과 관계등을 자체적인 문법으로 쉽게 맺고 할당할 수 있습니다.
        * 다양한 객체를 convention이란 약속 하에 RDBMS에 맺어줄 수 있습니다.

#### 티*
Q. 마크업을 할 떄 중요한 점이 뭐라고 생각하냐<br/>
Q. QA를 해봤다고 했는데 어떤 방식으로 진행을 했는가<br/>
Q. 보내준 코드에 대해서 설명해보세요<br/>
Q. 굳이 python을 이용하여 크롤링을 한 이유가 있는가?Ruby로 크롤링을 하지 않은 이유는?<br/>
Q. 당위성 체크가 어려웠다 했는데 당위성 체크는 어떻게 했는가?<br/>
Q. 코딩테스트 코드를 보면서 한번 짠 코드를 설명해보자<br/>
Q. 완성 못했던 부분은 어떻게 할 것인지 생각해보자<br/>
Q. 코드에 정규식이 나오는데 정규식에 대해 얘기해줄수있는가?<br/>
Q. Javascript scope chain은?<br/>
Q. Javascript prototype chaining?<br/>
Q. Javascript closures?<br/>
Q. Javascript 함수 호이스팅?


* 보내준 코드 설명 Gist[https://gist.github.com/hanjungv/b257752bc2995c2ebbf652cd65b85969](https://gist.github.com/hanjungv/b257752bc2995c2ebbf652cd65b85969)

* 굳이 Python으로 크롤링을 한 이유가 있는가? Ruby로도 할 수 있지 않나?
    * 추천 시스템은 read / write연산이 많고 따로 관계를 만들어 관리할 필요가 없기 때문에 빠른 mongoDB를 사용하려고 마음을 먹었다.
    * 루비로 많은 크롤링을 해본 경험이 있는 것도 아니었고
    * 파이썬에서 string을 파싱하는 코드들이 좀 더 쉽고 많았다.
        * ex> split 이나 문자열 슬라이싱 [0:3], find, index같은 기능들
    * 두개의 Databases환경을 왔다갔다 하기 좋은 건 python이 더 좋았다.
* 코딩 테스트 코드 완성한것
[https://github.com/hanjungv/tm_test](https://github.com/hanjungv/tm_test)
* 완성 못했던 부분은 어떻게 할 것인가?
    * 모든 데이터와 비교하였다. O(n)의 시간이 매번 들게 된다.
    * 되지 않는 경우를 체크 하면 총 4가지의 경우의 수가 나오고 되는 경우는 단순하게 두가지 정도만 된다. 되는 경우가 아니면 모두 되지 않는 경우니 2가지만 체크를 해주게 되었다.
    * 삭제와 업데이트의 validation부분은 db에서 체크를 해줘야 하지만 자바스크립트 단에서 userName과 생성자의 userName을 비교하는 형식으로 하였다. 실제로 보안을 할 때는 자바스크립트 단의 보안은 큰 힘이 되지 않는다. 스크립트를 끌 경우에 아무 힘도 못쓰고 열리게 된다. 스크립트단의 보안은 단순히 서버까지 왔다갔다 하는 시간을 줄이는 추가적인 편의 장치일 뿐이라고 생각한다.

* 마지막으로 읽은 책
    * 빅데이터가 만드는 세상
* 정규식은?

* JavaScript scope chain은?


### 그 외 개인적으로 물어볼만한것
Q. 편입 왜 했는가?<br/>
Q. 회사에서 왜 나왔는가?<br/>
Q. 학점이 생각보다 좋지 않다. 왜 그런가?<br/>
Q. 지금까지 당신은 성공적인 사례만을 들어 본인을 소개했는데, 당신이 실패한 사례에 관해 얘기해 주세요. 그 경험으로 당신은 무엇을 배웠나요?<br/>
Q. 마지막으로 물어보고 싶은거?<br/>
Q. 개인적인 디버깅방법?<br/>

### 혹시 페이로 면접을 보게 될 때 겪을 수 있는 사항들
* 1의보수, 2의 보수 
* 대규모 서비스에서 어떻게 로드를 분산할 지
* 페이 써봤나, 뭐가 불편한가
* 핀테크란?

### 소프트웨어 공학
* 아 수강을 안했네

### 준비를 해야 할 만한것
* 포트폴리오 하나 정도는 미리 만들어 놓는게 좋을 것 같다.


<br/><br/>