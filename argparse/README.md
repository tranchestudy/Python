argparse
========

python argparse 표준 라이브러리 관련한 내용을 정리했음

argparse 목적
-----------

options, arguments등을 쉽게 파싱할 수 있게 함으로써 command line
program을 쉽게 만들 수 있게 함.


간략 기능 소개
------------

필수 arguments와 options을 정의하면, argparse는 sys.argv에서 넘겨 받은
인자를 파싱해줌. help와 사용메시지등도 자동으로 생성해 주고 잘못된
arguments를 주는 경우 에러메시지도 생성을 해줌.

### 간략 사용 방법

* Creating a Parser 
~~~python3
>>> import argparse
>>> parser = argparse.ArgumentParser(description='Process some integers.')
~~~

* Adding arguments
~~~python3
>>> parser.add_argument('integers', metavar='N', type=int, nargs='+',
help='an integer for the accumulator')
~~~

* Parsing arguments
~~~python3
>>> parser.parse_args()    # 프로그램 실행시 인자로 받은 sys.argv를 파싱함
>>> parser.parse_args(['--sum', '7', '-1', '42'])  # 인자로 받은 list를 파싱함
~~~

add_argument() method
------------------------------------

```python3
ArgumentParser.add_argument(name or flags...[,action][,nargs][,const][,default][,type][,choices][,required][,help][,metavar][,dest])
```

* name or flags: option string의 이름 또는 목록. e.g. foo or -f, --foo
* action: command line에서 지정된 argument에 대한 action 지정
* nargs: 지정된 option string에서 사용할 command line argument 수. option string에 하나 이상의 값을 사용할 때 사용.
* const: 일부 action이나 nargs에서 요구되는 constant value
* default: command lin에서 argument가 생략되었을 때 사용되는 기본 값
* type: command line argument 변환되야 하는 type
* choices: argument에 사용될 값 목록
* required: command line에서 생략될 수 있는지 여부 (optional argument인 경우에만 사용)
* help: argument에 대한 간단한 설명
* metavar: usage message의 argument 이름
* dest: parse_args()로 생성된 객체에 추가될 attribute 이름.


References
----------

* [Python Standard Library](http://docs.python.org/3.4/library/argparse.html)
