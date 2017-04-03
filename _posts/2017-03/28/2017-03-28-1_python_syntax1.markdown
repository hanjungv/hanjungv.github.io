---

layout: post
title: "(PYTHON) Syntax[1]"
category: PYTHON

---

## 시작
뜻 밖의 파이썬 공부 시작이라 한번 코딩하면서 블로그에 정리하려 합니다.<br/>
잘못된 곳은 지적 부탁드립니다!

## 파이썬의 특징
* 러닝 커브가 매우 낮은 편이라고 합니다(배워봐야 알겠지만)
* 굉장히 직관적인 언어라고 합니다(이것도 배워봐야 알겠지만)

## 가장 기본적인 것들
* variable
    * Numbers : 다른 것들과 다른 표현들
    ~~~PYTHON
    >>> 8 // 5  # 이렇게 하면 작은 정수중 가장 큰 값으로 출력
    1
    >>> -7 // 3 # 이렇게 하면 -2가 아닌 -3
    -3
    >>> 5 ** 2  # 제곱수
    25
    >>> 2 ** 7  # 2 to the power of 7
    128
    # _ 는 마지막 계산한 값을 의미하는 것
    >>> price = 100.50
    >>> price
    100.5
    >>> price = price + _
    >>> price
    201.0
    ~~~
    * Strings
    ~~~PYTHON
    # 문자열 입력은 ""나 ''로 하면 된다.
    >>> a = "hello world"
    >>> b = " hanjungv"
    # multiline을 나타 낼 때는 """ 나 ''' 세개를 입력하면 된다.
    >>> c = """
    hanjungv
    ggg
    brbr
    """
    >>> c
    '\nhanjungv\nggg\nbrbr\n'
    # 이런것도 가능하다고 한다.
    >>> a+b
    'hello world hanjungv'
    >>> a*2
    'hello worldhello world'
    # 문자열 인덱싱
    >>> Hello = "Hello! My name is hanjung! Nice to meet you!"
    >>> len(Hello)
    44
    >>> Hello[-1]
    '!'
    >>> Hello[-4] # - 인덱싱이 가능하다..
    'y'
    # 문자열 슬라이싱
    >>> Hello[0:4]
    'Hell'
    >>> Hello[4:]
    'o! My name is hanjung! Nice to meet you!'
    >>> Hello[0:4] + Hello[4:]
    'Hello! My name is hanjung! Nice to meet you!'
    ~~~

    * 포매팅 : c와 비슷
    ~~~PYTHON
    >>> "hello world %s" % "hanjungv"
    'hello world hanjungv'
    >>> "hello world %d" % 3
    'hello world 3'
    >>> "hello world %f" % 3.4
    'hello world 3.400000'
    # 두개 이상 넣을 때는
    >>> "two argument %s, %d" % ("Hanjungv",40)
    'two argument Hanjungv, 40'

    # format메서드를 사용하면 쉽게 넣을 수 있다.
    >>> "Hello {0} world {1}".format("!","!!!")
    'Hello ! world !!!'
    >>> "Hello {a} world {b}".format(a="!",b="!!")
    'Hello ! world !!'
    ~~~
    * 관련 메서드 들
    ~~~PYTHON
    >>> a = "brown"
    # b의 갯수를 반환
    >>> a.count('b')
    1
    # Index 위치 반환
    >>> a.find('r')
    1
    >>> a.index('w')
    3
    # a 중간중간 'x'를 넣는다.
    >>> b = 'x'
    >>> b.join(a)
    'bxrxoxwxn'
    # 공백 자르기
    >>> a = '    br     '
    >>> a
    '    br     '
    >>> a.lstrip()
    'br     '
    >>> a.rstrip()
    '    br'
    >>> a.strip()
    'br'
    # 대체하기
    >>> b = "Hello tmdghks Hello jung"
    >>> b.replace("Hello", "Bye")
    'Bye tmdghks Bye jung'
    # split 하기
    >>> cr = "Hello:brbr:brbr"
    >>> cr.split()
    ['Hello:brbr:brbr']
    >>> cr.split(':')
    ['Hello', 'brbr', 'brbr']
    >>> dr = "Hello world"
    >>> dr.split()
    ['Hello', 'world']
    >>> dr.split(":")
    ['Hello world']
    ~~~
    * list
    ~~~PYTHON
    # 이런 느낌으로 사용이 가능하다
    >>> list2
    [1, 2, 3, [4, 5]]
    >>> list2[3][1]
    5
    # 리스트 또한 덧셈, 곱셈이 가능하다.
    >>> list1
    [1, 2, 3, 4, 5]
    >>> list2 = [1,2,3,[4,5]]
    [1,2,3,[4,5]]
    >>> list1 + list2
    [1, 2, 3, 4, 5, 1, 2, 3, [4, 5]]
    >>> list1*3
    [1, 2, 3, 4, 5, 1, 2, 3, 4, 5, 1, 2, 3, 4, 5]
    # del로 요소 지우기
    >>> del list1[2]
    >>> list1
    [1, 2, 4, 5]
    ~~~
    * 관련 메서드
    ~~~PYTHON

    ~~~
* control flows
* Functions
* Scope
* Loops


### 업데이트중

### 참조
* [참조사이트](https://docs.python.org/3/tutorial/introduction.html)
* [참조사이트2](https://wikidocs.net/13)

<br/><br/>
